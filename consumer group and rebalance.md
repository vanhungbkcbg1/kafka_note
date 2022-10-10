là quá trình phân bổ consumer cho các partition khi một add or delete consumer trong consumer group
##trong quá trình rebalance không có message nào được consume
consumer sẽ gửi tín hiệu headbeat tới broker, nếu trong thời gian mà consume ko gửi, thì được coi là ko khả dụng, quá trình rebalance sẽ sảy ra

