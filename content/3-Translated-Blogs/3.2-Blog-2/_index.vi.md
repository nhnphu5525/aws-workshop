---
title : "Blog 2"
date :  2025-09-10 
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

[**AWS Database Blog**](https://aws.amazon.com/blogs/database/)

## **Tính nhất quán dữ liệu với AWS DMS Data Resync**

by Suchindranath Hegde, Mahesh Kansara, and Sridhar Ramasubramanian |   on 09 SEP 2025 |   in [Advanced (300)](https://aws.amazon.com/blogs/database/category/learning-levels/advanced-300/), [AWS Database Migration Service](https://aws.amazon.com/blogs/database/category/database/aws-database-migration-service/), [Technical How-to](https://aws.amazon.com/blogs/database/category/post-types/technical-how-to/) |   [Permalink](https://aws.amazon.com/blogs/database/data-consistency-with-aws-dms-data-resync/) |   [Comments](https://aws.amazon.com/blogs/database/data-consistency-with-aws-dms-data-resync/#Comments) |   [Share](https://aws.amazon.com/vi/blogs/database/data-consistency-with-aws-dms-data-resync/#)

Trong bài viết này, chúng ta sẽ đi sâu vào **AWS Database Migration Service** (AWS DMS) Data Resync — một tính năng được giới thiệu trong phiên bản DMS 3.6.1 nhằm phát hiện và khắc phục data inconsistencies (sự không nhất quán dữ liệu) trong quá trình database migration, giúp loại bỏ nhu cầu can thiệp thủ công. Với **Data Resync**, bất kỳ data inconsistencies nào được phát hiện thông qua data validation giữa source database và target database đều sẽ được tự động xác định và xử lý.

Chúng ta sẽ cùng thảo luận về các bước kích hoạt tính năng Data Resync cũng như cách nó phát hiện và khắc phục sự không nhất quán dữ liệu thông qua các ví dụ minh họa.

Trước khi Data Resync được giới thiệu, việc xử lý data inconsistencies đòi hỏi sự can thiệp từ người dùng — chẳng hạn như thực hiện table reload trong tác vụ full load kết hợp với Change Data Capture (CDC), hoặc cập nhật thủ công các bản ghi trên target database.

Hiện nay, Data Resync đã khả dụng ở tất cả các AWS **Regions** nơi AWS DMS hỗ trợ migration từ Oracle hoặc SQL Server sang PostgreSQL hoặc **Amazon Aurora PostgreSQL-Compatible Edition.**

### **Cấu hình AWS DMS Data Resync**

Data Resync hoạt động bằng cách đọc các discrepancies (sai lệch dữ liệu) được xác định bởi DMS data validation, truy xuất current values từ source và áp dụng chúng lên target để đồng bộ bản ghi trên target. For a full load only task, resync, khi được bật, sẽ chạy ngay sau khi tất cả các bảng đã được validated. For tasks với CDC, resync phải được scheduled thông qua task settings, tại thời điểm đó task sẽ tạm dừng CDC và validation để giảm thiểu write conflicts.

Chúng tôi khuyến nghị bạn nên schedule các resync windows trong giai đoạn source database activity ở mức tối thiểu và trong khoảng thời gian ngắn, như được đề xuất trong **Best practices**. Điều này giúp giảm thiểu latency spikes do CDC bị tạm dừng.

Để configure data resync, bạn cần bật nó khi **creating** hoặc **modifying** a task. Trên AWS DMS console, trong phần **Data resync**, chọn **Schedule resync**, như minh họa trong ảnh chụp màn hình sau.

![Data Resync Configuration](/images/translated-blogs/blog2/pic1.png)

Lịch resync sử dụng Cron expression để lên lịch các lần chạy data resync:

```
* * * * *   
| | | | |   
| | | | |   
| | | | +---- Day of Week (0-6)   
| | | +------ Month (1-12)  
| | +-------- Day of Month (1-31)  
| +---------- Hour (0-23)  
+------------ Minute (0-59)
```

Ví dụ, các thiết lập sau lên lịch data resync chạy vào thứ Bảy lúc nửa đêm:

```json
"ResyncSettings":   
{  
    "EnableResync": true,  
    "ResyncSchedule": "0 0 * * 6", // Run Saturday at midnight  
    "MaxResyncTime": 360,  // Run for maximum of 360 minutes, or 6 hours  
    "ValidationTaskId": "" //Optional, used only if validation is performed as a separate Validation only task  
}
```

Để xem thêm ví dụ, tham khảo **Data resync configuration and examples.**

Với data resync, AWS DMS tạo một bảng **awsdms_validation_failures_v2** trên PostgreSQL target endpoint với cấu trúc được hiển thị trong ảnh chụp màn hình sau.

![Validation Failures Table](/images/translated-blogs/blog2/pic2.png)

Bảng này được tham chiếu để theo dõi và xử lý các mismatches trên các bảng target trong quá trình validation bằng cách tra cứu dữ liệu trên source sử dụng primary key. Khi upgrading hoặc di chuyển một task lên AWS DMS phiên bản 3.6.1 trở lên, các validation failures xảy ra trước khi nâng cấp sẽ không được resynced tự động. Để xử lý các upgrade validation failures, bạn cần initiate một table reload hoặc revalidation. Các validation failures mới xảy ra sau khi nâng cấp sẽ được theo dõi và resynced thông qua bảng awsdms_validation_failures_v2.

Trong quá trình resync operation, AWS DMS thực hiện tuần tự các bước sau, tùy thuộc vào task type. Các thông điệp sau có thể được tìm thấy trong CloudWatch logs cho từng bước, tùy thuộc vào task type:

**Đối với FULL LOAD and CDC hoặc CDC task:**

1. Kích hoạt resync operation:

```
[DATA_RESYNC ]I: Data Resync Manager schedule window time matched to start resync
```

2. Tạm dừng validation:

```
[DATA_RESYNC ]I: Trying to STOP validation before resync process. (resync_manager.c:331)
```

3. Tạm dừng CDC:

```
[DATA_RESYNC ]I: Data Resync Manager sending command to sorter to PAUSE applying changes to target.
```

4. Resync các bảng:

```
[RESYNC_UNLOAD ]I: Sent ctrl command for Resync Unload of table with id: 1
```

5. Tiếp tục CDC:

```
[DATA_RESYNC ]I: Data Resync Manager sending command to sorter to RESUME applying changes to target
```

6. Tiếp tục validation:

```
[DATA_RESYNC ]I: Trying to RESUME validation after resync process
```

**Đối với FULL LOAD only task**, bạn không cần chỉ định lịch (schedule) vì resync manager sẽ được kích hoạt sau khi quá trình validation hoàn tất:

1. Kích hoạt resync operation:

```
[DATA_RESYNC     ]I:  Data Resync Manager sending command to start up resync subtasks
```

2. Resync các bảng:

```
[TASK_MANAGER    ]I:  All tables are loaded. Validation is finished. Waiting for resync to finish...  (replicationtask.c:4953)  
[DATA_RESYNC     ]I:  Stopped Data Resync Manager, exiting thread
```

### **Các trường hợp sử dụng cho AWS DMS Data Resync**

Có một số use cases mà AWS DMS data resync trở nên hữu ích. Trong phần này, chúng ta sẽ xem xét hai trường hợp.

#### **Xóa nhầm các bản ghi trên target**

Trường hợp sử dụng đầu tiên mà chúng ta xem xét là khi các bản ghi trên target bị xóa nhầm. Để minh họa trường hợp này, chúng tôi thực hiện migration một bảng có tên REVIEWS từ Oracle sang PostgreSQL. Khi quá trình full load hoàn tất, chúng tôi vô tình xóa một vài bản ghi trên target. Trong ví dụ sau, chúng tôi sử dụng câu lệnh Data Manipulation Language (DML) trên target để xóa một bản ghi cụ thể trên target:

```sql
dmsdb=> delete from dms_test.reviews where review_id=8193;  
DELETE 1
```

Trong kịch bản này, việc cố gắng revalidate bảng sẽ dẫn đến mismatch, điều này có thể được xác nhận bằng cách nhập lệnh sau hoặc kiểm tra trên AWS console:

```bash
aws dms describe-table-statistics --replication-task-arn arn:aws:dms:us-east-1:xxxxxxxxxxxx:task:xxxxxxxxxxxx --filters Name=table-name,Values="REVIEWS"
```

```json
{  
    "TableStatistics": [  
        {  
            "SchemaName": "DMS_TEST",  
            "TableName": "REVIEWS",  
            "Inserts": 0,  
            "Deletes": 0,  
            "Updates": 0,  
            "Ddls": 0,  
            "AppliedInserts": 0,  
            "AppliedDeletes": 0,  
            "AppliedUpdates": 0,  
            "AppliedDdls": 0,  
            "FullLoadRows": 3500,  
            "FullLoadCondtnlChkFailedRows": 0,  
            "FullLoadErrorRows": 0,  
            "FullLoadStartTime": "2025-06-03T14:24:23.062000-05:00",  
            "FullLoadEndTime": "2025-06-03T14:24:25.408000-05:00",  
            "FullLoadReloaded": false,  
            "LastUpdateTime": "2025-06-03T14:35:12.009000-05:00",  
            "TableState": "Table completed",  
            "ValidationPendingRecords": 0,  
            "ValidationFailedRecords": 1,  
            "ValidationSuspendedRecords": 0,  
            "ValidationState": "Mismatched records"  
        }  
    ]  
}
```

Khi data resync được bật, các mismatches này sẽ được xử lý bằng cách kiểm tra source và sau đó reapply lên target. Trong ví dụ sau, chúng ta có thể xác nhận bản ghi được phản ánh trong bảng public.awsdms_validation_failures_v2, nơi nó đã được reapplied lên target, như được hiển thị bởi RESYNC_ACTION với giá trị UPSERT. RESYNC_TIME hiển thị timestamp khi hành động được thực hiện:

```sql
dmsdb=> select * from public.awsdms_validation_failures_v2;  
-[ RECORD 1 ]-+---------------------------  
RESYNC_ID     | 1029  
TASK_NAME     | BESR3KWW2FCLLH4AJBFSEYSNW4  
TABLE_OWNER   | dms_test  
TABLE_NAME    | reviews  
FAILURE_TIME  | 2025-06-03 19:33:26.410998  
KEY_TYPE      | Row  
KEY           | {                         +  
              |         "key":  ["8193"]  +  
              | }  
FAILURE_TYPE  | MISSING_TARGET  
DETAILS       |  
RESYNC_RESULT | SUCCESS  
RESYNC_TIME   | 2025-06-03 19:35:06.322  
RESYNC_ACTION | UPSERT
```

Hãy tưởng tượng một kịch bản trong đó chúng ta vô tình xóa thêm một vài bản ghi trên target trong quá trình CDC. Ví dụ, trong lệnh SQL sau, 20 bản ghi trên target bị xóa ngẫu nhiên:

```sql
dmsdb=> delete from dms_test.reviews where ctid in (select ctid from dms_test.reviews order by RANDOM() LIMIT 20);  
DELETE 20
```

Chúng ta có thể quan sát rằng data resync đã xử lý các bản ghi này và applied chúng thành công lên target:

```sql
dmsdb=> select "TABLE_OWNER", "TABLE_NAME","RESYNC_ACTION", "FAILURE_TYPE", "RESYNC_RESULT",count(*) from public.awsdms_validation_failures_v2 group by "TABLE_OWNER", "TABLE_NAME","RESYNC_ACTION", "FAILURE_TYPE", "RESYNC_RESULT";  
-[ RECORD 1 ]-+---------------  
TABLE_OWNER   | dms_test  
TABLE_NAME    | reviews  
RESYNC_ACTION | UPSERT 
FAILURE_TYPE  | MISSING_TARGET 
RESYNC_RESULT | SUCCESS 
count         | 21
```

Trong cả hai kịch bản full load và CDC mà chúng ta đã mô tả, data resync yêu cầu revalidation các bảng để tất cả các data inconsistencies được xác định và sửa chữa đúng cách. Việc revalidation này là cần thiết vì các thay đổi trên target không được thực hiện bởi AWS DMS.

#### **Tiếp tục task CDC sau khi xảy ra lỗi trên bảng**

Một trường hợp sử dụng khác có thể xảy ra trong quá trình migration khi một bảng ở trạng thái lỗi (error state) và các thay đổi của bảng đó sẽ không được replicated lên target. Khi một task đang chạy, bạn có thể **reload** một bảng. Tuy nhiên, đối với một CDC only task, bạn cần restart task từ LSN nơi bảng gặp lỗi. Nếu có nhiều bảng trong một AWS DMS task, việc start một DMS task từ một khoảng thời gian nhất định có thể dẫn đến việc reapplying changes lên target.

Hãy xem xét một kịch bản mà bạn migrate năm bảng thuộc ADMIN schema từ Oracle sang PostgreSQL. Trong ảnh chụp màn hình dưới đây, ba trong số năm bảng đã kết thúc ở trạng thái lỗi (error).

![Tables in Error State](/images/translated-blogs/blog2/pic3.png)

Bạn có thể nhận thấy từ CloudWatch logs rằng các bảng này đã kết thúc ở trạng thái lỗi (error) tại các timestamp khác nhau. Vì các bảng thất bại ở các timestamp khác nhau, bạn cần sử dụng earliest timestamp khi bảng gặp lỗi làm CDC start time và tạo một CDC only task với ba bảng này. Trong trường hợp này, earliest timestamp là 2025-06-05T03:40:13.

```
2025-06-05T03:40:13 [TASK_MANAGER ]W: Table 'ADMIN'.'DMST1' was errored/suspended (subtask 0 thread 1). 

2025-06-05T03:47:53 [TASK_MANAGER ]W: Table 'ADMIN'.'DMST2' was errored/suspended (subtask 0 thread 1). 

2025-06-05T03:52:32 [TASK_MANAGER ]W: Table 'ADMIN'.'DMST5' was errored/suspended (subtask 0 thread 1). 
```

![CDC Start Time](/images/translated-blogs/blog2/pic4.png)

Trong quá trình data resync, bạn có thể xác nhận rằng các conflicts được phát hiện đã được xử lý, như được hiển thị trong ảnh chụp màn hình sau.

![Resync Results](/images/translated-blogs/blog2/pic5.png)

```sql
dmsdb=> select * from public.awsdms_validation_failures_v2;  
-[ RECORD 1 ]-+---------------------------  
RESYNC_ID     | 9949  
TASK_NAME     | 6LOQBMAKQFDELB5WQB5BPG5Q74  
TABLE_OWNER   | admin  
TABLE_NAME    | dmst1  
FAILURE_TIME  | 2025-06-05 05:26:58.027987  
KEY_TYPE      | Row  
KEY           | {                         +  
              |         "key":  ["101"]   +  
              | }  
FAILURE_TYPE  | MISSING_TARGET  
DETAILS       |  
RESYNC_RESULT | SUCCESS  
RESYNC_TIME   | 2025-06-05 05:30:06.423  
RESYNC_ACTION | UPSERT
```

### **Kết luận**

Trong bài viết này, chúng tôi đã giới thiệu Data Resync, hướng dẫn cách configure nó và thảo luận về hai use cases mà chúng ta có thể sử dụng data resync để kiểm tra và sửa chữa các inconsistencies trong quá trình validation. Để biết thêm chi tiết, tham khảo **AWS DMS data resync**.

### **Về các tác giả**

**Suchindranath Hegde** là Senior Data Migration Specialist Solutions Architect tại Amazon Web Services. Anh ấy làm việc với khách hàng để cung cấp hướng dẫn và hỗ trợ kỹ thuật về data migration lên AWS Cloud sử dụng AWS DMS.

**Mahesh Kansara** là Database Engineering Manager tại Amazon Web Services. Anh ấy làm việc chặt chẽ với các nhóm phát triển và kỹ thuật để cải thiện dịch vụ migration và replication. Anh cũng làm việc với khách hàng để cung cấp hướng dẫn và hỗ trợ kỹ thuật về các dự án database và analytical, giúp họ nâng cao giá trị các giải pháp khi sử dụng AWS.

**Sridhar Ramasubramanian** là Database Engineer thuộc đội AWS Database Migration Service (DMS). Anh ấy làm việc để cải thiện dịch vụ DMS nhằm đáp ứng tốt hơn các nhu cầu của khách hàng AWS.
