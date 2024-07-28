import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int N = scanner.nextInt();
        int[] prices = new int[N];
        for (int i = 0; i < N; i++) {
            prices[i] = scanner.nextInt();
        }
        
        int[] spans = calculateSpan(prices);
        
        for (int span : spans) {
            System.out.print(span + " ");
        }
        System.out.print("END");
    }
    
    public static int[] calculateSpan(int[] prices) {
        int N = prices.length;
        int[] spans = new int[N];
        Stack<Integer> stack = new Stack<>();
        
        for (int i = 0; i < N; i++) {
            // Pop elements from stack while stack is not empty and the top of stack is less than or equal to current price
            while (!stack.isEmpty() && prices[stack.peek()] <= prices[i]) {
                stack.pop();
            }
            // If stack is empty, it means all previous elements are less than current price
            spans[i] = (stack.isEmpty()) ? (i + 1) : (i - stack.peek());
            // Push current index to stack
            stack.push(i);
        }
        
        return spans;
    }
}
