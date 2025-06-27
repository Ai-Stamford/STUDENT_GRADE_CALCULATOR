import 'dart:io';

void main() {
  print('UENR Student Grade Calculator');
  print('----------------------------\n');

  // Get student information
  stdout.write('Enter student name: ');
  String name = stdin.readLineSync()!;

  // Get assessment scores with validation
  double caScore = getValidScore('Enter Continuous Assessment score (0-30): ', 30);
  double examScore = getValidScore('Enter Exam score (0-50): ', 50);
  double projectScore = getValidScore('Enter Project score (0-20): ', 20);

  // Calculate total score
  double totalScore = caScore + examScore + projectScore;

  // Determine grade
  String grade = calculateGrade(totalScore);

  // Display results
  print('\n--- Results ---');
  print('Student: $name');
  print('CA Score: ${caScore.toStringAsFixed(1)}/30');
  print('Exam Score: ${examScore.toStringAsFixed(1)}/50');
  print('Project Score: ${projectScore.toStringAsFixed(1)}/20');
  print('Total Score: ${totalScore.toStringAsFixed(1)}/100');
  print('Final Grade: $grade');
}

double getValidScore(String prompt, int maxScore) {
  double score;
  while (true) {
    stdout.write(prompt);
    String input = stdin.readLineSync()!;
    try {
      score = double.parse(input);
      if (score < 0 || score > maxScore) {
        print('Error: Score must be between 0 and $maxScore');
      } else {
        return score;
      }
    } catch (e) {
      print('Error: Please enter a valid number');
    }
  }
}

String calculateGrade(double totalScore) {
  if (totalScore >= 80) return 'A';
  if (totalScore >= 75) return 'B+';
  if (totalScore >= 70) return 'B';
  if (totalScore >= 65) return 'C+';
  if (totalScore >= 60) return 'C';
  if (totalScore >= 55) return 'D+';
  if (totalScore >= 50) return 'D';
  return 'F';
}
