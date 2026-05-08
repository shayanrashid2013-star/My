import React, { useState, useEffect } from 'react'; import { View, Text, TouchableOpacity, StyleSheet, SafeAreaView, FlatList, Alert, } from 'react-native';

export default function App() { const [screen, setScreen] = useState('menu'); const [coins, setCoins] = useState(0); const [fishCaught, setFishCaught] = useState(0); const [memories, setMemories] = useState([]); const [festivalDay, setFestivalDay] = useState(1); const [energy, setEnergy] = useState(100);

useEffect(() => { const timer = setInterval(() => { setFestivalDay((prev) => prev + 1); }, 15000);

return () => clearInterval(timer);

}, []);

const catchFish = () => { const earned = Math.floor(Math.random() * 20) + 5; setCoins(coins + earned); setFishCaught(fishCaught + 1); setEnergy(Math.max(0, energy - 10));

Alert.alert(
  'Fishing Success 🎣',
  `Shin-chan caught a fish and earned ${earned} coins!`
);

};

const collectMemory = () => { const memoryList = [ 'Summer Fireworks', 'Beach Sunset', 'Lantern Festival', 'Funny Shiro Moment', 'Family Dinner', 'Cloud Garden Adventure', ];

const randomMemory =
  memoryList[Math.floor(Math.random() * memoryList.length)];

setMemories([...memories, randomMemory]);
setCoins(coins + 10);

Alert.alert('Memory Collected ✨', randomMemory);

};

const glideLantern = () => { const reward = Math.floor(Math.random() * 30) + 10;

setCoins(coins + reward);
setEnergy(Math.max(0, energy - 15));

Alert.alert(
  'Lantern Gliding ☁️',
  `You explored the skies and earned ${reward} coins!`
);

};

const rest = () => { setEnergy(100); Alert.alert('Rest Time 💤', 'Shin-chan feels refreshed!'); };

if (screen === 'menu') { return ( <SafeAreaView style={styles.container}> <View style={styles.heroBox}> <Text style={styles.title}> Shin chan: Sky Lantern City </Text>

<Text style={styles.subtitle}>
        A cozy summer adventure above the clouds.
      </Text>

      <TouchableOpacity
        style={styles.button}
        onPress={() => setScreen('game')}
      >
        <Text style={styles.buttonText}>Start Adventure</Text>
      </TouchableOpacity>
    </View>
  </SafeAreaView>
);

}

return ( <SafeAreaView style={styles.gameContainer}> <Text style={styles.header}>☁️ Sky Lantern City</Text>

<View style={styles.statsBox}>
    <Text style={styles.stat}>🪙 Coins: {coins}</Text>
    <Text style={styles.stat}>🎣 Fish: {fishCaught}</Text>
    <Text style={styles.stat}>⚡ Energy: {energy}</Text>
    <Text style={styles.stat}>🎉 Festival Day: {festivalDay}</Text>
  </View>

  <TouchableOpacity style={styles.actionButton} onPress={catchFish}>
    <Text style={styles.actionText}>🎣 Go Fishing</Text>
  </TouchableOpacity>

  <TouchableOpacity
    style={styles.actionButton}
    onPress={collectMemory}
  >
    <Text style={styles.actionText}>✨ Collect Memory</Text>
  </TouchableOpacity>

  <TouchableOpacity style={styles.actionButton} onPress={glideLantern}>
    <Text style={styles.actionText}>☁️ Lantern Gliding</Text>
  </TouchableOpacity>

  <TouchableOpacity style={styles.actionButton} onPress={rest}>
    <Text style={styles.actionText}>💤 Rest</Text>
  </TouchableOpacity>

  <View style={styles.memorySection}>
    <Text style={styles.memoryTitle}>Collected Memories</Text>

    <FlatList
      data={memories}
      keyExtractor={(item, index) => index.toString()}
      renderItem={({ item }) => (
        <View style={styles.memoryCard}>
          <Text style={styles.memoryText}>✨ {item}</Text>
        </View>
      )}
    />
  </View>
</SafeAreaView>

); }

const styles = StyleSheet.create({ container: { flex: 1, backgroundColor: '#FFD9A0', justifyContent: 'center', alignItems: 'center', padding: 20, }, heroBox: { backgroundColor: '#FFFFFF', width: '100%', borderRadius: 25, padding: 30, alignItems: 'center', elevation: 8, }, title: { fontSize: 32, fontWeight: 'bold', textAlign: 'center', color: '#FF6B00', marginBottom: 15, }, subtitle: { fontSize: 18, textAlign: 'center', color: '#444', marginBottom: 30, }, button: { backgroundColor: '#FF6B00', paddingVertical: 15, paddingHorizontal: 35, borderRadius: 20, }, buttonText: { color: '#FFF', fontSize: 20, fontWeight: 'bold', }, gameContainer: { flex: 1, backgroundColor: '#DFF6FF', padding: 15, }, header: { fontSize: 30, fontWeight: 'bold', textAlign: 'center', color: '#005B96', marginBottom: 20, }, statsBox: { backgroundColor: '#FFFFFF', borderRadius: 20, padding: 15, marginBottom: 20, }, stat: { fontSize: 18, marginBottom: 5, color: '#333', }, actionButton: { backgroundColor: '#4DA8DA', padding: 16, borderRadius: 18, marginBottom: 12, alignItems: 'center', }, actionText: { color: '#FFF', fontSize: 18, fontWeight: 'bold', }, memorySection: { flex: 1, marginTop: 10, }, memoryTitle: { fontSize: 22, fontWeight: 'bold', color: '#222', marginBottom: 10, }, memoryCard: { backgroundColor: '#FFFFFF', padding: 14, borderRadius: 15, marginBottom: 10, }, memoryText: { fontSize: 16, color: '#333', }, });

/*

HOW TO BUILD APK

1. Install Node.js


2. Install Expo CLI:



npm install -g expo-cli

3. Create Project:



npx create-expo-app shinchan-game

4. Replace App.js with this file.


5. Run:



npm install npx expo start

6. Build APK:



npx eas build -p android --profile preview

7. Download APK from Expo build link.



============================== OPTIONAL FEATURES TO ADD

Character movement

Multiplayer festivals

Cloud island map

Save/load system

Sound effects

Anime cutscenes

Inventory system

NPC dialogue

Fishing animations


*/
