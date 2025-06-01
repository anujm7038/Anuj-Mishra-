# Anuj-Mishra-
import React, { useState } from 'react';
import { StyleSheet, Text, View, TextInput, Button, Alert } from 'react-native';

export default function App() {
  const [numberToGuess, setNumberToGuess] = useState(Math.floor(Math.random() * 100) + 1);
  const [guess, setGuess] = useState('');
  const [message, setMessage] = useState('Guess a number between 1 and 100');

  const handleGuess = () => {
    const guessedNumber = parseInt(guess);
    if (isNaN(guessedNumber)) {
      Alert.alert('Please enter a valid number');
      return;
    }
    if (guessedNumber === numberToGuess) {
      setMessage(`Congratulations! You guessed the number ${numberToGuess}!`);
    } else if (guessedNumber < numberToGuess) {
      setMessage('Try higher!');
    } else {
      setMessage('Try lower!');
    }
    setGuess('');
  };

  const resetGame = () => {
    setNumberToGuess(Math.floor(Math.random() * 100) + 1);
    setMessage('Guess a number between 1 and 100');
    setGuess('');
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Guess The Number Game</Text>
      <Text style={styles.message}>{message}</Text>
      <TextInput
        style={styles.input}
        keyboardType="numeric"
        value={guess}
        onChangeText={setGuess}
        placeholder="Enter your guess"
      />
      <Button title="Guess" onPress={handleGuess} />
      <Button title="Reset Game" onPress={resetGame} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: 'center', alignItems: 'center', backgroundColor: '#fff' },
  title: { fontSize: 24, fontWeight: 'bold', marginBottom: 20 },
  message: { fontSize: 18, marginBottom: 20 },
  input: { height: 40, borderColor: 'gray', borderWidth: 1, width: '60%', marginBottom: 20, textAlign: 'center' },
});
