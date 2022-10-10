khi comsumer consume message from broker, nó sẽ tự động gửi một mesage vào một topic đặc biệt : __consumer_offsets
for cho mỗ partition
nó sẽ không có vấn đề gì khi tất cả các consumer đều hoạt động tốt, không có consumer nào bị die or crash
trường hợp mà có consumer bị die or crash thì quá trình rebalance sẽ sảy ra, consumer sẽ được assign số lượng partition khác so với   
trước đó nó được assign, để biết được  sẽ bắt đầu sử lí ở message nào thì nó dựa trên last commit  offset của mỗi partition
và bắt đầu xử lí từ vị trí này 
