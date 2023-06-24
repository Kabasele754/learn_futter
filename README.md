# Apprendre Dart

Dart est un langage optimisé pour le client permettant de développer des applications rapides sur n'importe quelle plate-forme. Son objectif est d'offrir le langage de programmation le plus productif pour le développement multiplateforme, associé à une plate-forme d'exécution d'exécution flexible pour les frameworks d'applications.

Les langages sont définis par leur enveloppe technique - les choix effectués au cours du développement qui façonnent les capacités et les points forts d'un langage. Dart est conçu pour une enveloppe technique particulièrement adaptée au développement client, en donnant la priorité à la fois au développement (rechargement à chaud avec état en moins d'une seconde) et aux expériences de production de haute qualité sur une grande variété de cibles de compilation (web, mobile et bureau).

Dart constitue également la base de Flutter . Dart fournit le langage et les runtimes qui alimentent les applications Flutter, mais Dart prend également en charge de nombreuses tâches de développement de base telles que le formatage, l'analyse et le test du code.

# Le langage dart

Le langage Dart est de type sécurisé ; il utilise la vérification de type statique pour s'assurer que la valeur d'une variable correspond toujours au type statique de la variable. Parfois, on parle de typage sonore. Bien que les types soient obligatoires, les annotations de type sont facultatives en raison de l'inférence de type. Le système de typage Dart est également flexible, permettant l'utilisation d'un dynamictype combiné à des contrôles d'exécution, ce qui peut être utile lors d'expérimentations ou pour un code qui doit être particulièrement dynamique.

Dart a une sécurité intégrée pour le son nul . Cela signifie que les valeurs ne peuvent pas être nulles, sauf si vous dites qu'elles peuvent l'être. Avec une sécurité nulle solide, Dart peut vous protéger des exceptions nulles lors de l'exécution grâce à l'analyse statique du code. Contrairement à de nombreux autres langages null-safe, lorsque Dart détermine qu'une variable n'accepte pas les valeurs nulles, cette variable ne peut jamais être nulle. Si vous inspectez votre code en cours d'exécution dans le débogueur, vous constatez que la non-nullabilité est conservée au moment de l'exécution ; d'où sa sécurité nulle.

L'exemple de code suivant présente plusieurs fonctionnalités du langage Dart, notamment les bibliothèques, les appels asynchrones, les types nullables et non nullables, la syntaxe des flèches, les générateurs, les flux et les getters. Pour en savoir plus sur la langue, faites le Dart language tour .

```
import 'dart:math' show Random;

void main() async {
  print('Compute π using the Monte Carlo method.');
  await for (final estimate in computePi().take(100)) {
    print('π ≅ $estimate');
  }
}

/// Generates a stream of increasingly accurate estimates of π.
Stream<double> computePi({int batch = 100000}) async* {
  var total = 0; // Inferred to be of type int
  var count = 0;
  while (true) {
    final points = generateRandom().take(batch);
    final inside = points.where((p) => p.isInsideUnitCircle);

    total += batch;
    count += inside.length;
    final ratio = count / total;

    // Area of a circle is A = π⋅r², therefore π = A/r².
    // So, when given random points with x ∈ <0,1>,
    // y ∈ <0,1>, the ratio of those inside a unit circle
    // should approach π / 4. Therefore, the value of π
    // should be:
    yield ratio * 4;
  }
}

Iterable<Point> generateRandom([int? seed]) sync* {
  final random = Random(seed);
  while (true) {
    yield Point(random.nextDouble(), random.nextDouble());
  }
}

class Point {
  final double x;
  final double y;

  const Point(this.x, this.y);

  bool get isInsideUnitCircle => x * x + y * y <= 1;
}
```
