---
layout: post
title:  "Design Pattern - Oberver"
date:   2019-08-14 21:03:36 +0530
tags: "design pattern observer software architecture java"
---
Observer Pattern dịnh nghĩa sự phụ thuộc một-nhiều giữa các đối tượng sao cho khi một đối tượng thay đổi trạng thái thì tất cả các đối tượng phụ thuộc nó cũng thay đổi theo, tần suất sử dụng cao. *"Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically."*

## 1. Vấn đề (Problem):

Cách bản của bạn vài cây số có một cửa hàng (Store) bán đồ công nghệ. Sản phẩm mới về cửa hàng một ngày bất kì mà không có lịch cụ thể. Bạn không muốn thường xuyên tới (Store) và hỏi xem có sản phẩm mới nào không thay vào đó muốn nhận được thông báo mỗi khi có sản phẩm mới. Cửa hàng không thể gửi thông báo (Notification) tới mọi người trong bản của bạn vì sẽ làm phiền mọi người. Vậy cần có cơ chế để giải quyết vấn đề trên.   
Hình ảnh: [refactoring.guru](https://refactoring.guru)
![observer-comic!](/assets/images/design_pattern/observer-comic.png)

---
## 2. Giải quyết (solution):
### 2.1. Ý tưởng (idea)
Mỗi khách hàng có lựa chọn đăng kí nhận thông báo mỗi khi có sản phẩm mới về cửa hàng hay là không

### 2.2. Thiết kế (architecture)
![observer-class-diagram!](/assets/images/design_pattern/observer-class-diagram.png)

### 2.3. Triển khai (implementation)
MObserverable.java
```java
public interface MObserverable  {
    public void updateNotification(String msg);
    public String showInfo();
}
```

MClient.java
```java
public class MClient implements MObserverable {
    private String m_name;

    public MClient(String name) {
        this.m_name = name;
    }

    @Override
    public void updateNotification(String msg) {
        System.out.println(this.m_name + " recieve: " + msg);
    }

    @Override
    public String showInfo() {
        return m_name;
    }
}
```

MStore.java
```java
public class MStore {
    private ArrayList<MObserverable> m_observables = null;
    
    public MStore(){
        m_observables = new ArrayList<>();
    }

    public void subscribe(MObserverable observable)
    {
        m_observables.add(observable);
        System.out.println(observable.showInfo() + " subscribe ++");
    }

    public void unsubscribe(MObserverable observable){
        if(m_observables.contains(observable))
        {
            m_observables.remove(observable);
            System.out.println(observable.showInfo() + " unsubscribe --");
        }
    }

    public void notifyAllSubscriber(String msg){
        System.out.println("Store notify all:" + msg);
        for (MObserverable observer : m_observables) {
            observer.updateNotification(msg);
        }
    }
}
```

MainObserver.java
```java
public class MainObserver {

    public static void main(String[] args) {
       System.out.println("Observer Pattern Demo");
       MStore store = new MStore();

       MClient client1 = new MClient("Le Van Manh");
       MClient client2 = new MClient("Nguyen Anh Tuan");
       MClient client3 = new MClient("Nguyen Khac Khu");
       MClient client4 = new MClient("Nguyen Thi Thao");

       store.subscribe(client1);
       store.notifyAllSubscriber("Have new model Galaxy A50");
       store.subscribe(client2);
       store.notifyAllSubscriber("Have new model Galaxy A60");
       store.unsubscribe(client1);
       store.subscribe(client3);
       store.subscribe(client4);
       store.notifyAllSubscriber("Have new model Galaxy A70");
    }
}
```

Kết quả chạy chương trình
```yml
Observer Pattern Demo
Le Van Manh subscribe ++
Store notify all:Have new model Galaxy A50
Le Van Manh recieve: Have new model Galaxy A50
Nguyen Anh Tuan subscribe ++
Store notify all:Have new model Galaxy A60
Le Van Manh recieve: Have new model Galaxy A60
Nguyen Anh Tuan recieve: Have new model Galaxy A60
Le Van Manh unsubscribe --
Nguyen Khac Khu subscribe ++
Nguyen Thi Thao subscribe ++
Store notify all:Have new model Galaxy A70
Nguyen Anh Tuan recieve: Have new model Galaxy A70
Nguyen Khac Khu recieve: Have new model Galaxy A70
Nguyen Thi Thao recieve: Have new model Galaxy A70
```
---
## 3. Observer Pattern (structure):
Các bạn học java rồi thì sẽ thấy nó chính là cơ chế listener trong java, ngoài ra chúng ta có thể tự liên hệ sang nhiều cái khác tùy vào khả năng tưởng tượng mỗi người. Dưới đây là một kiến trúc chung của observer pattern.   
Hình ảnh [refactoring.guru](https://refactoring.guru)   
![observer-class-diagram-theory!](/assets/images/design_pattern/observer-class-diagram-theory.png)

**Publisher(Store)**: Đối tượng thực hiện việc cung cấp thông tin theo yêu cầu.   
**Oberver(Listener)**: Đối tượng tiếp nhận thông tin dưới góc nhìn của publisher, trong một vài trường hợp nó còn có tên là listener chuyên dùng để lắng nghe. Giống như việc bạn để lại thông tin cho cửa hàng chứ không phải để lại body ở đó.  
**Subcriber(Person)**: Đối tượng nhận thông tin từ publisher.

---
## Tài liệu tham khảo (reference):  
[http://www.uml.org.cn/c++/pdf/DesignPatterns.pdf](http://www.uml.org.cn/c++/pdf/DesignPatterns.pdf)   
[https://refactoring.guru/design-patterns/observer](https://refactoring.guru/design-patterns/observer)   
[https://blog.duyet.net/2015/02/design-pattterns-he-thong-23-mau-design.html](https://blog.duyet.net/2015/02/design-pattterns-he-thong-23-mau-design.html)   
