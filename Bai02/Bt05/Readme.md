
 Thông tin bài làm
- Tên bài: AnimateApp
- **Mô tả:** Ứng dụng theo dõi mục tiêu học tập với hiệu ứng animation khi hoàn thành.
- **Link Expo:https://snack.expo.dev/@duyanhdepzai/animateapp

 Cấu trúc Component
1. **ProgressCard.js** — Hiển thị thông tin mục tiêu và thanh tiến độ
````
code
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function ProgressCard({ title, current, total }) {
  const percentage = Math.round((current / total) * 100);

  return (
    <View style={styles.card}>
      <Text style={styles.title}>{title}</Text>
      <View style={styles.progressBarBg}>
        <View style={[styles.progressBarFill, { width: `${percentage}%` }]} />
      </View>
      <Text style={styles.text}>{current} / {total} — {percentage}%</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  card: {
    backgroundColor: '#fff',
    borderRadius: 16,
    padding: 24,
    marginBottom: 20,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 8,
    elevation: 4,
  },
  title: {
    fontSize: 18,
    fontWeight: '600',
    marginBottom: 12,
    color: '#333',
  },
  progressBarBg: {
    height: 12,
    backgroundColor: '#e0e0e0',
    borderRadius: 6,
    overflow: 'hidden',
    marginBottom: 8,
  },
  progressBarFill: {
    height: '100%',
    backgroundColor: '#2196F3',
    borderRadius: 6,
  },
  text: {
    fontSize: 14,
    color: '#666',
  },
});
````
2. **ActionButton.js** — Nút bấm thực hiện hành động
 ```
code
import React from 'react';
import { TouchableOpacity, Text, StyleSheet } from 'react-native';

export default function ActionButton({ title, onPress }) {
  return (
    <TouchableOpacity style={styles.button} onPress={onPress} activeOpacity={0.8}>
      <Text style={styles.text}>{title}</Text>
    </TouchableOpacity>
  );
}

const styles = StyleSheet.create({
  button: {
    backgroundColor: '#2196F3',
    paddingVertical: 14,
    paddingHorizontal: 32,
    borderRadius: 12,
    alignItems: 'center',
  },
  text: {
    color: '#fff',
    fontSize: 16,
    fontWeight: '600',
  },
});
```` 
3. **AnimatedMessage.js** — Thông báo có hiệu ứng phóng to/hiện ẩn
```
code
import React, { useRef, useEffect } from 'react';
import { View, Text, StyleSheet, Animated, Easing } from 'react-native';

export default function AnimatedMessage({ visible, message }) {
  const scaleValue = useRef(new Animated.Value(0)).current;
  const opacityValue = useRef(new Animated.Value(0)).current;

  useEffect(() => {
    if (visible) {
      Animated.parallel([
        Animated.timing(scaleValue, {
          toValue: 1,
          duration: 500,
          easing: Easing.elastic(1.2),
          useNativeDriver: true,
        }),
        Animated.timing(opacityValue, {
          toValue: 1,
          duration: 400,
          useNativeDriver: true,
        }),
      ]).start();
    } else {
      Animated.parallel([
        Animated.timing(scaleValue, {
          toValue: 0,
          duration: 300,
          useNativeDriver: true,
        }),
        Animated.timing(opacityValue, {
          toValue: 0,
          duration: 300,
          useNativeDriver: true,
        }),
      ]).start();
    }
  }, [visible, scaleValue, opacityValue]);

  if (!visible && scaleValue._value === 0) return null;

  return (
    <Animated.View
      style={[
        styles.container,
        {
          transform: [{ scale: scaleValue }],
          opacity: opacityValue,
        },
      ]}
    >
      <Text style={styles.text}>🎉 {message}</Text>
    </Animated.View>
  );
}

const styles = StyleSheet.create({
  container: {
    marginTop: 24,
    padding: 20,
    backgroundColor: '#4CAF50',
    borderRadius: 12,
    alignItems: 'center',
  },
  text: {
    color: '#fff',
    fontSize: 16,
    fontWeight: '600',
  },
});
````
## Giao diện trước khi hoàn thành
- Thanh tiến độ chưa đầy, nút hiển thị "Bắt đầu / Tiến hành", không có thông báo.
  Kết quả :
  <img width="333" height="580" alt="image" src="https://github.com/user-attachments/assets/ae7357f3-ca73-40c8-8686-1234943c08b0" />


## Giao diện khi hoàn thành
- Thanh tiến độ đạt 100%, nút đổi thành "Đã hoàn thành", thông báo mừng hiện ra với hiệu ứng phóng to mượt mà.
  Kết quả :
  <img width="328" height="579" alt="image" src="https://github.com/user-attachments/assets/b8b201f7-98b5-43e9-8ecf-8e2fc4cd8e85" />


## Hình ảnh ban đầu:
<img width="319" height="606" alt="image" src="https://github.com/user-attachments/assets/fd9cbf92-b9e0-4d97-8352-b4a2fc16aa99" />



