# plant_store_ui
import 'package:flutter/material.dart';

void main() {
  runApp(const PlantStoreApp());
}

class PlantStoreApp extends StatelessWidget {
  const PlantStoreApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: const HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        leading: const Icon(Icons.menu),
        actions: [
          IconButton(onPressed: () {}, icon: const Icon(Icons.shopping_cart)),
        ],
      ),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            const Text(
              "Hello Gayatri 👋",
              style: TextStyle(fontSize: 22, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 10),
            TextField(
              decoration: InputDecoration(
                hintText: "Search plants",
                prefixIcon: const Icon(Icons.search),
                border: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(20),
                ),
              ),
            ),
            const SizedBox(height: 15),
            // Categories
            SizedBox(
              height: 40,
              child: ListView(
                scrollDirection: Axis.horizontal,
                children: const [
                  CategoryChip(title: "Popular"),
                  CategoryChip(title: "Outdoor"),
                  CategoryChip(title: "Indoor"),
                  CategoryChip(title: "Top Pick"),
                ],
              ),
            ),
            const SizedBox(height: 15),
            // Plant list
            Expanded(
              child: ListView(
                scrollDirection: Axis.horizontal,
                children: const [
                  PlantCard(
                    name: "Aloe Vera",
                    price: "\$25",
                    imageUrl:
                        "https://upload.wikimedia.org/wikipedia/commons/e/e8/Aloe_vera_flower_inset.JPG",
                  ),
                  PlantCard(
                    name: "Snake Plant",
                    price: "\$30",
                    imageUrl:
                        "https://upload.wikimedia.org/wikipedia/commons/2/2c/Snake_plant.jpg",
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}

class CategoryChip extends StatelessWidget {
  final String title;
  const CategoryChip({super.key, required this.title});

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: const EdgeInsets.only(right: 10),
      padding: const EdgeInsets.symmetric(horizontal: 16, vertical: 8),
      decoration: BoxDecoration(
        color: Colors.green[100],
        borderRadius: BorderRadius.circular(20),
      ),
      child: Text(title),
    );
  }
}

class PlantCard extends StatelessWidget {
  final String name, price, imageUrl;
  const PlantCard(
      {super.key,
      required this.name,
      required this.price,
      required this.imageUrl});

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) => PlantDetailScreen(
              name: name,
              price: price,
              imageUrl: imageUrl,
            ),
          ),
        );
      },
      child: Container(
        width: 160,
        margin: const EdgeInsets.only(right: 15),
        child: Column(
          children: [
            Hero(
              tag: name,
              child: ClipRRect(
                borderRadius: BorderRadius.circular(20),
                child: Image.network(imageUrl, height: 120, fit: BoxFit.cover),
              ),
            ),
            const SizedBox(height: 5),
            Text(name, style: const TextStyle(fontWeight: FontWeight.bold)),
            Text(price, style: const TextStyle(color: Colors.green)),
          ],
        ),
      ),
    );
  }
}

class PlantDetailScreen extends StatelessWidget {
  final String name, price, imageUrl;
  const PlantDetailScreen(
      {super.key, required this.name, required this.price, required this.imageUrl});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        leading: const BackButton(),
        actions: [
          IconButton(onPressed: () {}, icon: const Icon(Icons.favorite_border)),
        ],
      ),
      body: Column(
        children: [
          Hero(
            tag: name,
            child: Image.network(imageUrl, height: 200),
          ),
          const SizedBox(height: 10),
          Text(name,
              style: const TextStyle(fontSize: 24, fontWeight: FontWeight.bold)),
          Text(price, style: const TextStyle(fontSize: 20, color: Colors.green)),
          const SizedBox(height: 20),
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: const [
              Icon(Icons.wb_sunny, color: Colors.orange),
              Icon(Icons.water_drop, color: Colors.blue),
              Icon(Icons.thermostat, color: Colors.red),
            ],
          ),
          const SizedBox(height: 20),
          const Padding(
            padding: EdgeInsets.all(16),
            child: Text(
              "This is a beautiful plant. It needs light, water, and care.",
              textAlign: TextAlign.center,
            ),
          ),
        ],
      ),
    );
  }
}
