1，使用pageHelp和swagger—ui都需要注入bean，configration中配置数据。

2，打包发布需要配置相应的jar包。

3，创建项目，需要添加对应的jar包

4，测试类需要每条添加注释和相应的Junit依赖

一，观察者模式

观察者模式又被称为发布/订阅模式，在对象之间定义了一对多的依赖，这样一来，当一个对象改变的时候，所有的对象都会接收到结果。

二，核心角色

抽象被观察者角色

抽象观察者角色

具体被观察者角色

具体观察者角色

三，java内置观察者模式的实现

在java.util中包含了Observer接口和Observerable抽象类。

1，定义具体被观察者

package com.dpb.observer2;

import java.util.Observable;

/**
 * 目标对象
 * 继承 Observable
 * @author dengp
 *
 */
public class ConcreteSubject extends Observable {
	
	private int state; 
	
	public void set(int s){
		state = s;  //目标对象的状态发生了改变
		setChanged();  //表示目标对象已经做了更改
		notifyObservers(state);  //通知所有的观察者
	}

	public int getState() {
		return state;
	}

	public void setState(int state) {
		this.state = state;
	}
}
2，定义具体观察者
package com.dpb.observer2;

import java.util.Observable;
import java.util.Observer;
/**
 * 观察者模式：观察者(消息订阅者)
 * 实现Observer接口
 * @author dengp
 *
 */
public class ObserverA implements Observer {

	private int myState;
	
	@Override
	public void update(Observable o, Object arg) {
		myState = ((ConcreteSubject)o).getState();
	}
	public int getMyState() {
		return myState;
	}
	public void setMyState(int myState) {
		this.myState = myState;
	}
}

