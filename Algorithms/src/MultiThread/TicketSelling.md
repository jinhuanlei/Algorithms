## Simulate Ticket Selling

Two ways to implement multiple thread.
1. extends Thread
1. implements Runnable

Code:
```java
class TicketSelling implements Runnable{
    private int TICKET = 100;
    
    @Override
    public void run() {
        while(TICKET > 0){
            System.out.println("Selling one ticket, cur amount" + TICKET--);
        }
    }

    public static void main(String[] args) {
        TicketSelling ts = new TicketSelling();
        new Thread(ts).run();
        new Thread(ts).run();
        new Thread(ts).run();
        new Thread(ts).run();
        new Thread(ts).run();
        new Thread(ts).run();
    }

}
```