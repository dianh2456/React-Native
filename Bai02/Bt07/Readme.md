Link:

https://snack.expo.dev/@duyanhdepzai/bookingapp

App.js

  Vai trò:
  
import ...	Tải các thư viện và màn hình cần sử dụng

createNativeStackNavigator()	Tạo ra đối tượng quản lý luồng màn hình theo kiểu "ngăn xếp" (mở màn hình mới chồng lên trên)

<NavigationContainer>	Bao bọc toàn bộ ứng dụng, là ngữ cảnh cho hệ thống điều hướng

<Stack.Navigator>	Khai báo cấu hình chung cho thanh tiêu đề (màu nền, chữ, vị trí)

<Stack.Screen name="..." component={...} />	Đăng ký từng màn hình:

• name: Tên gọi tắt để chuyển màn hình

• component: Component hiển thị

• options: Cấu hình hiển thị thanh tiêu đề

• headerLeft: () => null: Ẩn nút quay lại ở màn hình xác nhận

```
code
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import HomeScreen from './screens/HomeScreen';
import ServiceDetailScreen from './screens/ServiceDetailScreen';
import BookingScreen from './screens/BookingScreen';
import ConfirmationScreen from './screens/ConfirmationScreen';

const Stack = createNativeStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator
        initialRouteName="Home"
        screenOptions={{
          headerStyle: { backgroundColor: '#2563eb' },
          headerTintColor: '#fff',
          headerTitleStyle: { fontWeight: 'bold' },
          headerTitleAlign: 'center',
        }}
      >
        <Stack.Screen
          name="Home"
          component={HomeScreen}
          options={{ title: 'Trang chủ' }}
        />
        <Stack.Screen
          name="ServiceDetail"
          component={ServiceDetailScreen}
          options={{ title: 'Chi tiết dịch vụ' }}
        />
        <Stack.Screen
          name="Booking"
          component={BookingScreen}
          options={{ title: 'Đặt lịch hẹn' }}
        />
        <Stack.Screen
          name="Confirmation"
          component={ConfirmationScreen}
          options={{ title: 'Xác nhận đặt lịch', headerLeft: () => null }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

ServiceCard.js

- Vai trò: Hiển thị thông tin tóm tắt mỗi dịch vụ trên trang chủ
- Nội dung: Hình ảnh, tên, thời lượng, giá; có thể nhấn để xem chi tiết
```
code
import { View, Text, Image, StyleSheet, Pressable } from 'react-native';

export default function ServiceCard({ service, onPress }) {
  return (
    <Pressable style={styles.card} onPress={onPress}>
      <Image source={{ uri: service.image }} style={styles.image} />
      <View style={styles.info}>
        <Text style={styles.name}>{service.name}</Text>
        <Text style={styles.duration}>⏱ {service.duration}</Text>
        <Text style={styles.price}>{service.price} VNĐ</Text>
      </View>
    </Pressable>
  );
}

const styles = StyleSheet.create({
  card: {
    flexDirection: 'row',
    backgroundColor: '#fff',
    borderRadius: 12,
    padding: 12,
    marginBottom: 12,
    shadowColor: '#000',
    shadowOpacity: 0.1,
    shadowRadius: 6,
    elevation: 3,
  },
  image: { width: 80, height: 80, borderRadius: 8, marginRight: 12 },
  info: { flex: 1, justifyContent: 'center' },
  name: { fontSize: 16, fontWeight: 'bold', marginBottom: 4 },
  duration: { fontSize: 14, color: '#666', marginBottom: 4 },
  price: { fontSize: 15, color: '#2563eb', fontWeight: '600' },
});
```

