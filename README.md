# Lab-Report
```java
class SharedCounter {
    private int counter = 0;

    public synchronized int increment() {
        counter++;
        return counter;
    }
}

class NumberThread extends Thread {
    SharedCounter counter;

    NumberThread(SharedCounter counter) {
        this.counter = counter;
    }

    @Override
    public void run() {
        try {
            for (int i = 1; i <= 10; i++) {
                System.out.println("NumberThread: " + i + " s Counter: " + counter.increment());
                Thread.sleep(500);
            }
        } catch (InterruptedException e) {
            System.out.println(e);
        }
    }
}

class SquareRunnable implements Runnable {
    SharedCounter counter;

    SquareRunnable(SharedCounter counter) {
        this.counter = counter;
    }

    @Override
    public void run() {
        try {
            for (int i = 1; i <= 10; i++) {
                System.out.println("SquareThread: " + (i * i) + "  Counter: " + counter.increment());
                Thread.sleep(500);
            }
        } 
        catch (InterruptedException e) {
            System.out.println(e);
        }
    }
}

public class MultithreadingDemo {
    public static void main(String[] args) {

        SharedCounter counter = new SharedCounter();

        NumberThread thread1 = new NumberThread(counter);
        Thread thread2 = new Thread(new SquareRunnable(counter));

        thread1.start();
        thread2.start();
    }
}
```
