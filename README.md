# CALCULATOR

import React, { useState } from 'react';
import {
  StyleSheet,
  Text,
  View,
  TouchableOpacity,
  SafeAreaView,
} from 'react-native';

export default function App() {
  const [result, setResult] = useState('');

  const handlePress = (value) => {
    if (value === '=') {
      try {
        setResult(eval(result).toString());
      } catch (error) {
        setResult('Error');
      }
    } else if (value === 'C') {
      setResult('');
    } else {
      setResult(result + value);
    }
  };

  const buttons = [
    ['C', '(', ')', '/'],
    ['7', '8', '9', '*'],
    ['4', '5', '6', '-'],
    ['1', '2', '3', '+'],
    ['0', '.', '='],
  ];

  return (
    <SafeAreaView style={styles.container}>
      {/* Display Screen */}
      <View style={styles.screen}>
        <Text style={styles.resultText}>{result || '0'}</Text>
      </View>

      {/* Button Grid */}
      <View style={styles.buttonContainer}>
        {buttons.map((row, rowIndex) => (
          <View key={rowIndex} style={styles.row}>
            {row.map((button, buttonIndex) => (
              <TouchableOpacity
                key={buttonIndex}
                style={[
                  styles.button,
                  button === '=' ? styles.equalButton : null,
                  button === 'C' ? styles.clearButton : null,
                ]}
                onPress={() => handlePress(button)}
              >
                <Text style={styles.buttonText}>{button}</Text>
              </TouchableOpacity>
            ))}
          </View>
        ))}
      </View>

      {/* Footer */}
      <View style={styles.footer}>
        <Text style={styles.footerText}>Designed by Satyam</Text>
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f0f0f0',
  },
  screen: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'flex-end',
    backgroundColor: '#222',
    padding: 20,
    borderBottomLeftRadius: 20,
    borderBottomRightRadius: 20,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.2,
    shadowRadius: 3,
    elevation: 5,
  },
  resultText: {
    fontSize: 48,
    fontWeight: 'bold',
    color: '#fff',
  },
  buttonContainer: {
    flex: 3,
    padding: 10,
  },
  row: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 15,
  },
  button: {
    flex: 1,
    margin: 5,
    height: 70,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#333',
    borderRadius: 35,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.3,
    shadowRadius: 3,
    elevation: 5,
  },
  buttonText: {
    fontSize: 24,
    fontWeight: '600',
    color: '#fff',
  },
  equalButton: {
    backgroundColor: '#28a745',
  },
  clearButton: {
    backgroundColor: '#d9534f',
  },
  footer: {
    padding: 15,
    alignItems: 'center',
    backgroundColor: '#333',
    borderTopLeftRadius: 20,
    borderTopRightRadius: 20,
  },
  footerText: {
    fontSize: 18,
    fontWeight: 'bold',
    color: '#fff',
  },
});
