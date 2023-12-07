---
layout: post
title:  "Design Pattern - Command"
date:   2019-09-21 21:03:36 +0530
tags: "design pattern commad software architecture java"
---

Đóng gói yêu cầu thành một đối tượng, bằng cách đó cho phép bạn tham số hóa client với các yêu cầu khác nhau, hàng đợi hoặc nhật kí yêu cầu, hỗ trợ các phương thức undo.*"Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations."*

## 1. Vấn đề (Problem):
## 2. Giải quyết (Solution):
### 2.1 Ý tưởng (idea)
### 2.2 Thiết kế (architecture)
![uml_implement_class_diagram!](/assets/images/design_pattern/command_pattern/uml_implement_class_diagram.png)
### 2.3 Triển khai (implementation)
Command.java
```java
public interface Command {

    public abstract void excute();
}
```

Light.java
```java
public class Light {

    public void turnOn(){
        System.out.println("Light Turn On.");
    }

    public void turnOff(){
        System.out.println("Light Turn Off.");
    }
}
```

TurnOnCommand.java
```java
public class TurnOnCommand implements Command{
    private Light light = null;
    public TurnOnCommand(Light light){
        this.light = light;
    }

    @Override
    public void excute() {
        this.light.turnOn();
    }
    
}
```
TurnOffCommand.java
```java
public class TurnOffCommand implements Command{
    Light light = null;
    public TurnOffCommand(Light light){
        this.light = light;
    }
    @Override
    public void excute() {
        this.light.turnOff();
    }
}
```

RemoteControl.java
```java
public class RemoteControl {
    ArrayList<Command> listCommand = null;
    public RemoteControl(){
        this.listCommand = new ArrayList<Command>();
    }
    public void addCommand(Command cmd){
        this.listCommand.add(cmd);
    }
    public void remote(){
        for (Command cmd : this.listCommand) {
            cmd.excute();
        }
    }
}
```

```java
public class Client {

    public static void main(String[] args) {
        System.out.println("Command Pattern Demo.");
        Light light = new Light();
        RemoteControl control = new RemoteControl();
        TurnOnCommand onCommand = new TurnOnCommand(light);
        TurnOffCommand offCommand = new TurnOffCommand(light);
        control.addCommand(onCommand);
        control.addCommand(offCommand);
        control.remote();
    }
}
```
Kết quả chạy chương trình
```yml
Command Pattern Demo.
Light Turn On.
Light Turn Off.
```
## 3. Command Pattern (structure):
## Tài liệu tham khảo (reference):