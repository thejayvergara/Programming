// IMPORTS
import java.util.*;

public class LearningJava {
    public static void main(String args[]) {
        // VARIABLES
        int integerNumber;
        double doubleNumber;
        boolean isTrue;
        String message;

        // OUTPUT
        System.out.print();
        System.out.println();

        // INPUT
        Scanner input = new Scanner(System.in);
        integerNumber = input.nextInt();
        doubleNumber = input.nextDouble();

        // IF ELSE STATEMENT
        if () {

        } else {

        }

        // COMPARING FLOAT VALUES
        final double EPSILON = 1E-14;
        double x = 1.0 - 0.1 - 0.1 - 0.1 - 0.1 - 0.1;
        if (Math.abs(x - 0.5) < EPSILON)
            System.out.println(x + "is approximately 0.5");

        // RANDOM NUMBERS
        (int)(Math.random() * 10); // Generates 0 - 9

        // TERMINATE PROGRAM
        System.exit(0);

        // SWITCH STATEMENT
        switch () {
            case 0:
                break;
            default:
                break;
        }

        // CONDITIONAL OPERATOR
        // bool ? ifTrue : ifFalse;
        turnedOn = isOn ? yes : no;
}