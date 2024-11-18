# SOLID Principles;
SOLID Principles are a set of design principles that help developers build software that is easier to understand, maintain, and extend. Adhering to these principles ensures high-quality, scalable, and robust code.

1. Improved Code Maintainability
SOLID principles break code into smaller, more manageable pieces.
Changes in one part of the system are less likely to affect other parts, reducing the risk of bugs.

2. Enhances Scalability
Software becomes easier to extend with new features without modifying existing code.
This ensures that future requirements can be incorporated smoothly.

3. Encourages Reusability
Well-structured code can be reused in different parts of the application or even across projects.
Reduces redundancy and effort in the long run.

6. Reduces Complexity
Divides responsibilities across classes and methods, leading to cleaner and simpler designs.
Easier to understand and navigate through the codebase.

5. Facilitates Unit Testing
Code adhering to SOLID principles is loosely coupled, making it easier to test individual components.
Helps ensure high-quality software delivery.

   1) SRP - SINGLE RESPONSIBILTY PRINCIPLE:-
        A class/package/application should have one and only one reason to change.
   Example:
                  public class Tast{
                              public void downloadFile(String location);
                              public void parseFile(File file);
                              public void persistTheDate(Data data);
                      }
  
   2)  Open/Closed Principle (OCP)
       The Open/Closed Principle is one of the five SOLID principles in object-oriented programming. It states:

"A class should be open for extension but closed for modification."

This means you should be able to add new functionality to a class without altering its existing code. By adhering to this principle, you reduce the risk of introducing bugs in the existing system and make your codebase easier to maintain and extend.

Example :

Without OCP (Violation):
Imagine you have a system where you're calculating discounts for different customer types (e.g., Regular and Premium).

                        class DiscountCalculator {
                            public double calculateDiscount(String customerType, double amount) {
                                if (customerType.equals("Regular")) {
                                    return amount * 0.1; // 10% discount for Regular
                                } else if (customerType.equals("Premium")) {
                                    return amount * 0.2; // 20% discount for Premium
                                }
                                return 0;
                            }
                        }
Problem:
If you need to add a new customer type (e.g., "VIP"), you must modify the calculateDiscount method, breaking the Open/Closed Principle.

With OCP (Solution):
You can refactor the code to adhere to the OCP by using polymorphism:

Define a common interface:

                                interface DiscountStrategy {
                                    double calculateDiscount(double amount);
                                }
                                Implement strategies for each customer type:
                                java
                                Copy code
                                class RegularDiscount implements DiscountStrategy {
                                    public double calculateDiscount(double amount) {
                                        return amount * 0.1; // 10% discount for Regular
                                    }
                                }
                                
                                class PremiumDiscount implements DiscountStrategy {
                                    public double calculateDiscount(double amount) {
                                        return amount * 0.2; // 20% discount for Premium
                                    }
                                }
                                
                                class VIPDiscount implements DiscountStrategy {
                                    public double calculateDiscount(double amount) {
                                        return amount * 0.3; // 30% discount for VIP
                                    }
                                }
Use the strategy dynamically:

                              class DiscountCalculator {
                                  private DiscountStrategy discountStrategy;
                              
                                  public DiscountCalculator(DiscountStrategy discountStrategy) {
                                      this.discountStrategy = discountStrategy;
                                  }
                              
                                  public double calculateDiscount(double amount) {
                                      return discountStrategy.calculateDiscount(amount);
                                  }
                              }
Example Usage:

                              public class Main {
                                  public static void main(String[] args) {
                                      DiscountCalculator regularCalculator = new DiscountCalculator(new RegularDiscount());
                                      System.out.println("Regular Discount: " + regularCalculator.calculateDiscount(1000));
                              
                                      DiscountCalculator premiumCalculator = new DiscountCalculator(new PremiumDiscount());
                                      System.out.println("Premium Discount: " + premiumCalculator.calculateDiscount(1000));
                              
                                      DiscountCalculator vipCalculator = new DiscountCalculator(new VIPDiscount());
                                      System.out.println("VIP Discount: " + vipCalculator.calculateDiscount(1000));
                                  }
                              }
Benefits:

Extensible: Adding new discount types doesn't require modifying the existing code, just adding new classes.
Maintainable: Existing functionality remains unaffected, reducing the chances of bugs.
Adheres to OCP: Classes are open for extension (new discount types) but closed for modification. 


 
   3) Liskov Substitution Principle (LSP):

The Liskov Substitution Principle (LSP) is the "L" in the SOLID principles of object-oriented programming. It states:

"Objects of a superclass should be replaceable with objects of its subclass without affecting the correctness of the program."

In simpler terms, a subclass should be able to do everything its parent class can do, without altering the expected behavior.

Example Without LSP:

                                  class Bird {
                                      public void fly() {
                                          System.out.println("Flying...");
                                      }
                                  }
                                  
                                  class Sparrow extends Bird {
                                      // Sparrow is fine, it can fly.
                                  }
                                  
                                  class Ostrich extends Bird {
                                      // Ostrich cannot fly.
                                      @Override
                                      public void fly() {
                                          throw new UnsupportedOperationException("Ostrich cannot fly.");
                                      }
                                  }
                                  
                                  public class Main {
                                      public static void main(String[] args) {
                                          Bird bird = new Ostrich(); // Using Ostrich as a Bird
                                          bird.fly(); // Throws exception, breaking the LSP.
                                      }
                                  }
Here, the substitution of Ostrich for Bird causes unexpected behavior because Ostrich cannot fly. This violates the LSP.

Example Following LSP:

                                          // Corrected design
                                          abstract class Bird {
                                              // General bird properties and behaviors
                                          }
                                          
                                          abstract class FlyingBird extends Bird {
                                              public abstract void fly();
                                          }
                                          
                                          class Sparrow extends FlyingBird {
                                              @Override
                                              public void fly() {
                                                  System.out.println("Sparrow flying...");
                                              }
                                          }
                                          
                                          class Ostrich extends Bird {
                                              // Ostrich does not fly but is still a Bird.
                                          }
                                          
                                          public class Main {
                                              public static void main(String[] args) {
                                                  FlyingBird bird = new Sparrow();
                                                  bird.fly(); // Works fine.
                                          
                                                  Bird ostrich = new Ostrich();
                                                  // No fly method, no unexpected behavior.
                                              }
                                          }
Explanation of Fixed Example:
Separated Bird into FlyingBird and non-flying birds.
Now, only flying birds like Sparrow implement the fly method.
Ostrich doesn’t break expectations as it does not implement fly.




4)   Interface Segregation Principle (ISP) :

   The Interface Segregation Principle states:
"A client should not be forced to implement interfaces it does not use."

This means that instead of creating large, bloated interfaces with multiple unrelated methods, it’s better to create smaller, more specific interfaces tailored to the needs of individual clients.

Why is ISP Important?
Avoids forcing classes to implement unnecessary methods.
Reduces code complexity and makes systems more maintainable.
Encourages better design by promoting cohesive interfaces.
Simple Example: Interface Segregation Principle

Problem: Without ISP
Imagine you have an interface for various types of workers:


                                            public interface Worker {
                                                void work();
                                                void eat();
                                            }
                                            Now, both a HumanWorker and a RobotWorker implement this interface:
                                            
                                            
                                            public class HumanWorker implements Worker {
                                                @Override
                                                public void work() {
                                                    System.out.println("Human is working.");
                                                }
                                            
                                                @Override
                                                public void eat() {
                                                    System.out.println("Human is eating.");
                                                }
                                            }
                                            
                                            public class RobotWorker implements Worker {
                                                @Override
                                                public void work() {
                                                    System.out.println("Robot is working.");
                                                }
                                            
                                                @Override
                                                public void eat() {
                                                    // Robots don't eat!
                                                    throw new UnsupportedOperationException("Robots don't eat.");
                                                }
                                            }
Here, RobotWorker is forced to implement the eat() method even though it doesn’t need it. This violates the ISP.

Solution: With ISP
We split the Worker interface into two smaller interfaces:


                              public interface Workable {
                                  void work();
                              }
                              
                              public interface Eatable {
                                  void eat();
                              }
Now, each class implements only the interface it needs:

                        public class HumanWorker implements Workable, Eatable {
                            @Override
                            public void work() {
                                System.out.println("Human is working.");
                            }
                        
                            @Override
                            public void eat() {
                                System.out.println("Human is eating.");
                            }
                        }
                        
                        public class RobotWorker implements Workable {
                            @Override
                            public void work() {
                                System.out.println("Robot is working.");
                            }
                        }
Benefits of ISP in This Example : 
HumanWorker uses both work() and eat() methods, so it implements both interfaces.
RobotWorker only needs the work() method, so it implements only the Workable interface.
No unnecessary methods are forced upon the classes, adhering to ISP.


 
