# 几个前端框架的比较

## 一、几个框架修改数据的不同

#### Vue

1. 创建一个数据对象，其中的数据可以自由更改。

> this.name = 'a' 赋值。this.name = 'b'，更改。

#### React

1. 创建一个状态对象，更改数据需要更多的操作。

2. 例如：this.status(...)

3. React之所以使用状态的方式，是为了方便在数据进行了改变之后，及时追踪和运行声明周期hook。

> this.state.name = 'a' 赋值。 this.setState({ name:'b' })。