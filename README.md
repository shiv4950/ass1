*********************************************audio,vlc****************************************************
#audioplayer.j
package Pac1;

public interface AudioPlayer {
	void play(String audioType, String fileName);

}
#AudioPlayerAdapter.java
package Pac1;

public class AudioPlayerAdapter implements AudioPlayer {
	
	 MediaPlayer mediaPlayer;

	    @Override
	    public void play(String audioType, String fileName) {
	        if (audioType.equalsIgnoreCase("mp4")) {
	            mediaPlayer = new MP4Player();
	        } else if (audioType.equalsIgnoreCase("vlc")) {
	            mediaPlayer = new VLCPlayer();
	        } else {
	            System.out.println("Invalid media type: " + audioType);
	            return;
	        }
	        mediaPlayer.play(fileName);
	    }

}

#Main.java

package Pac1;

public class Main {

	public static void main(String[] args) {
        AudioPlayer audioPlayer = new AudioPlayerAdapter();
        audioPlayer.play("mp3", "song.mp3");
        audioPlayer.play("mp4", "video.mp4");
        audioPlayer.play("vlc", "movie.vlc");
    }
}

#MediaPlayer.java
package Pac1;

public interface MediaPlayer {
	
	void play(String fileName);

}

#MP4Player.java
package Pac1;

public class MP4Player implements MediaPlayer {
	
	@Override
    public void play(String fileName) {
        System.out.println("Playing mp4: " + fileName);
    }

}

#SimpleAudioPlayer.java
package Pac1;

public class SimpleAudioPlayer implements AudioPlayer {
	
	@Override
    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("mp3")) {
            System.out.println("Playing mp3: " + fileName);
        } else {
            System.out.println("Invalid media type: " + audioType);
        }
    }

}

#VLCPlayer.java
package Pac1;

public class VLCPlayer implements MediaPlayer {
	
	@Override
    public void play(String fileName) {
        System.out.println("Playing vlc: " + fileName);
    }

}
**********************************************employe manager****************************************************************
#Employee.java
package Pac2;


import java.util.ArrayList;
import java.util.List;

public interface Employee {
	
	void showDetails();

}

#IndividualEmployee.java
package Pac2;

public class IndividualEmployee implements Employee {
	
	 private String name;
	    private String role;

	    public IndividualEmployee(String name, String role) {
	        this.name = name;
	        this.role = role;
	    }

	    @Override
	    public void showDetails() {
	        System.out.println("Employee Name: " + name + ", Role: " + role);
	    }

}

#Main.java
package Pac2;

public class Main {
    public static void main(String[] args) {
        // Create individual employees
        Employee emp1 = new IndividualEmployee("Alice", "Developer");
        Employee emp2 = new IndividualEmployee("Bob", "Designer");
        
        // Create a manager
        Manager manager = new Manager("Charlie", "Development Manager");

        // Add employees to the manager's team
        manager.addEmployee(emp1);
        manager.addEmployee(emp2);
        
        // Create another manager
        Manager generalManager = new Manager("David", "General Manager");
        
        // Create a few more employees
        Employee emp3 = new IndividualEmployee("Eve", "QA Tester");
        
        // Add manager and employees to the general manager
        generalManager.addEmployee(manager);
        generalManager.addEmployee(emp3);
        
        // Show the structure
        System.out.println("Reporting Structure:");
        generalManager.showDetails();
    }
}


#Maneger.java
package Pac2;
import java.util.*;


public class Manager implements Employee{
	
	 private String name;
	    private String role;
	    private List<Employee> teamMembers;

	    public Manager(String name, String role) {
	        this.name = name;
	        this.role = role;
	        this.teamMembers = new ArrayList<>();
	    }

	    public void addEmployee(Employee employee) {
	        teamMembers.add(employee);
	    }

	    public void removeEmployee(Employee employee) {
	        teamMembers.remove(employee);
	    }

	    @Override
	    public void showDetails() {
	        System.out.println("Manager Name: " + name + ", Role: " + role);
	        System.out.println("Team Members:");
	        for (Employee employee : teamMembers) {
	            employee.showDetails();
	        }
	    }

}


************************************shapes**********************************************************************************************
#Circle.java
package Pac3;

public class Circle extends Shape {
 private double x, y, radius;

 public Circle(double x, double y, double radius, DrawingAPI drawingAPI) {
     super(drawingAPI);
     this.x = x;
     this.y = y;
     this.radius = radius;
 }

 public void draw() {
     drawingAPI.drawCircle(x, y, radius);
 }

 public void resize(double percent) {
     radius *= percent;
 }
}


#DrawingAPI.java
package Pac3;

public interface DrawingAPI {
	
 void drawCircle(double x, double y, double radius);
 void drawRectangle(double x, double y, double width, double height);
 
}


#DrawingAPI1.java
package Pac3;

public class DrawingAPI1 implements DrawingAPI {
 public void drawCircle(double x, double y, double radius) {
     System.out.printf("DrawingAPI1.circle at (%.1f, %.1f) radius %.1f%n", x, y, radius);
 }

 public void drawRectangle(double x, double y, double width, double height) {
     System.out.printf("DrawingAPI1.rectangle at (%.1f, %.1f) width %.1f height %.1f%n", x, y, width, height);
 }
}


#DrawingAPI2.java
package Pac3;


public class DrawingAPI2 implements DrawingAPI {
	 public void drawCircle(double x, double y, double radius) {
	     System.out.printf("DrawingAPI2.circle at (%.1f, %.1f) radius %.1f%n", x, y, radius);
	 }

	 public void drawRectangle(double x, double y, double width, double height) {
	     System.out.printf("DrawingAPI2.rectangle at (%.1f, %.1f) width %.1f height %.1f%n", x, y, width, height);
	 }
	}

#Main.java
package Pac3;

public class Main {
 public static void main(String[] args) {
     Shape circle1 = new Circle(5, 10, 2, new DrawingAPI1());
     Shape rectangle1 = new Rectangle(1, 2, 3, 4, new DrawingAPI2());

     circle1.draw();
     rectangle1.draw();

     circle1.resize(2);
     rectangle1.resize(1.5);

     circle1.draw();
     rectangle1.draw();
 }
}

#Rectangle.java
package Pac3;

public class Rectangle extends Shape {
	 private double x, y, width, height;

	 public Rectangle(double x, double y, double width, double height, DrawingAPI drawingAPI) {
	     super(drawingAPI);
	     this.x = x;
	     this.y = y;
	     this.width = width;
	     this.height = height;
	 }

	 public void draw() {
	     drawingAPI.drawRectangle(x, y, width, height);
	 }

	 public void resize(double percent) {
	     width *= percent;
	     height *= percent;
	 }
	}

#Shape.java
package Pac3;

public abstract class Shape {
 protected DrawingAPI drawingAPI;

 protected Shape(DrawingAPI drawingAPI) {
     this.drawingAPI = drawingAPI;
 }

 public abstract void draw(); // abstract method to draw the shape
 public abstract void resize(double percent); // abstract method to resize the shape
}


**********************************pizza*********************************************
#BasicPizza.java
package Pac4;


public class BasicPizza implements Pizza {
 @Override
 public String getDescription() {
     return "Basic Pizza";
 }

 @Override
 public double cost() {
     return 8.00; 
 }
}


#cheese.java
package Pac4;

public class Cheese extends PizzaDecorator {
 public Cheese(Pizza pizza) {
     super(pizza);
 }

 @Override
 public String getDescription() {
     return pizza.getDescription() + ", Cheese";
 }

 @Override
 public double cost() {
     return pizza.cost() + 1.50;
 }
}



#Main.java
package Pac4;

public class Main {
 public static void main(String[] args) {
     Pizza pizza = new BasicPizza();
     System.out.println(pizza.getDescription() + " $" + pizza.cost());

     pizza = new Cheese(pizza);
     System.out.println(pizza.getDescription() + " $" + pizza.cost());

     pizza = new Olives(pizza);
     System.out.println(pizza.getDescription() + " $" + pizza.cost());

     pizza = new Mushrooms(pizza);
     System.out.println(pizza.getDescription() + " $" + pizza.cost());
 }
}

#Mushrooms.java
package Pac4;


public class Mushrooms extends PizzaDecorator {
public Mushrooms(Pizza pizza) {
   super(pizza);
}

@Override
public String getDescription() {
   return pizza.getDescription() + ", Mushrooms";
}

@Override
public double cost() {
   return pizza.cost() + 1.25; 
}
}


#Olives.java
package Pac4;


public class Mushrooms extends PizzaDecorator {
public Mushrooms(Pizza pizza) {
   super(pizza);
}

@Override
public String getDescription() {
   return pizza.getDescription() + ", Mushrooms";
}

@Override
public double cost() {
   return pizza.cost() + 1.25; 
}
}

#pizza.java
}

#PizzaDecorator.java
package Pac4;


public abstract class PizzaDecorator implements Pizza {
 protected Pizza pizza;

 public PizzaDecorator(Pizza pizza) {
     this.pizza = pizza;
 }

 @Override
 public String getDescription() {
     return pizza.getDescription();
 }

 @Override
 public double cost() {
     return pizza.cost();
 }
}

********************************
