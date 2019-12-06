During the exam of ADS you have an ingenious idea of sorting the questions based on the amount of points you can obtain per question. 
Using this approach you will first tackle the questions that can reward you with the most points, before attempting the other questions.

In this exercise you will need to finish the constructor of the Exam class, which takes as input an array of ExamQuestions, as well as the method getNext which returns the next question that needs to be answered. 
In the library, you can find the implementation of the class ExamQuestion.

### Library
```java
class ExamQuestion implements Comparable<ExamQuestion> {

  // The question number
  private int id;

  // The number of points that can be obtained by answering this question
  private int value;

  public ExamQuestion(int id, int value) {
    this.id = id;
    this.value = value;
  }

  /**
   * Compares two exam questions by comparing their values.
   * Can be used to sort the exam questions in descending order.
   * @param that - other exam question
   * @return
   */
  @Override
  public int compareTo(ExamQuestion that) {
    // By swapping the position of this and that, we will sort in ascending order.
    return Integer.compare(that.value, this.value);
  }

  public int getId() {
    return this.id;
  }

  public int getValue() {
    return this.value;
  }
}

```


### Solution
```java
import java.util.*;

class Exam {
  Queue<ExamQuestion> q;

  /**
   * Constructor
   * @param questions - the questions that are part of this exam
   */
  public Exam(ExamQuestion[] questions) {
     q = new PriorityQueue<>();
    for(ExamQuestion eq : questions)
      q.add(eq);
  }

  /**
   * Returns the next question that should be answered on this exam,
   * the values of the returned exam questions should in descending order (i.e. questions with high value should be returned first)
   * @return
   */
  public ExamQuestion getNext() {
    return q.poll();
  }
}
```
