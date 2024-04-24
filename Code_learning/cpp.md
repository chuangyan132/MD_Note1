# CPP_code_learning
## Ros2 book
### Chapter 1
#### std::shared_ptr<rclcpp::Node> node = std::make_shared<rclcpp::Node>("simple_node");
##### This line manually creates a new instance of rclcpp::Node and then constructs a std::shared_ptr to manage it. This is not the recommended way to create a shared_ptr because it can lead to exceptions not being caught and potential memory leaks if the new operation succeeds but the shared_ptr constructor throws an exception. preferred Method Using std::make_shared
#####  std::shared_ptr<rclcpp::Node> node = std::make_shared<rclcpp::Node>("simple_node");
