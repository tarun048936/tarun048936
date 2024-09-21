public class IntegerToWord {
    private static final String[] units = {"", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"};
    private static final String[] teens = {"ten", "eleven", "twelve", "thirteen", "fourteen", "fifteen", "sixteen", "seventeen", "eighteen", "nineteen"};
    private static final String[] tens = {"", "", "twenty", "thirty", "forty", "fifty", "sixty", "seventy", "eighty", "ninety"};
    private static final String[] thousands = {"", "thousand", "million", "billion"};

    public static String numberToWord(int num) {
        if (num == 0) return "zero";

        int i = 0;
        String words = "";

        while (num > 0) {
            if (num % 1000 != 0) {
                words = helper(num % 1000) + " " + thousands[i] + (words.isEmpty() ? "" : " ") + words;
            }
            num /= 1000;
            i++;
        }

        return words.trim();
    }

    private static String helper(int num) {
        if (num == 0) return "";

        if (num < 10) return units[num];
        if (num < 20) return teens[num - 10];
        if (num < 100) return tens[num / 10] + (num % 10 == 0 ? "" : " " + units[num % 10]);

        return units[num / 100] + " hundred" + (num % 100 == 0 ? "" : " and " + helper(num % 100));
    }

    public static void main(String[] args) {
        System.out.println(numberToWord(1000)); // Output: one thousand
        System.out.println(numberToWord(4003)); // Output: four thousand three
    }
}
