đọc message từ queue
đọc message theo thứ tự message đã đẩy vào trong queue,consumer sẽ lưu lại vị trí mà message đã được đọc 

#### consumer nằm trong consumer group,một consumer group thì đọc message trong một topic
- consumer group đảm bảo một partition trong một topic tại một thời điểm chỉ có một member của group được đọc message
- khi consumer join vao consumer group no se duoc assign toi 1 partition, va no se dam nhan viec consume message tren partition do
  khi consumer leave khoi group, thi qua trinh rebalance se dien ra, de phan bo partition cho nhung worker con lai

single kafka server là một broker
một partition có thể được replicate ra nhiều broker khác nhau   
a partition is owned by a singer broker in the cluster, and that broker is called leader of that partition
#### tat cả các phương thức của producer và consumer phải được thực hiện thông qua leader

#### mỗi một topic sẽ có dung lương lưu trữ nhất định, khi dung lượng đó được chạm tới thì message sẽ bị mất,broker sẽ cho phetp setting time retention cho từng topic

## trường hợp có 1 group consumer
##### case 1
![image1](https://www.oreilly.com/api/v2/epubs/9781491936153/files/assets/ktdg_04in01.png)
##### case 2
![image 2](https://www.oreilly.com/api/v2/epubs/9781491936153/files/assets/ktdg_04in02.png)
##### case 3
![image 3](https://www.oreilly.com/api/v2/epubs/9781491936153/files/assets/ktdg_04in03.png)
##### case 4
![image 4](https://www.oreilly.com/api/v2/epubs/9781491936153/files/assets/ktdg_04in04.png)

## trường hợp có nhiều consumer group cùng read message trên 1 topic, thì các consumer group sẽ độc lập, không phụ thuộc vào consume hiện tại đang làm gì
![image](https://learning.oreilly.com/library/view/kafka-the-definitive/9781491936153/assets/ktdg_04in05.png)
