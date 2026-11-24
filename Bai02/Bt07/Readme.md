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

 DateSelector.js

- **Vai trò**: Tạo giao diện chọn ngày trong tuần tới
- **Nội dung**: Tự động tạo danh sách 7 ngày kế tiếp; đánh dấu ngày đang chọn
```
code
import { View, Text, Pressable, StyleSheet } from 'react-native';

export default function DateSelector({ selectedDate, onSelectDate }) {
  const dates = Array.from({ length: 7 }, (_, i) => {
    const d = new Date();
    d.setDate(d.getDate() + i);
    return {
      value: d.toISOString().split('T')[0],
      day: d.toLocaleDateString('vi-VN', { weekday: 'short' }),
      date: d.getDate(),
    };
  });

  return (
    <View style={styles.container}>
      <Text style={styles.label}>Chọn ngày:</Text>
      <View style={styles.list}>
        {dates.map((item) => (
          <Pressable
            key={item.value}
            style={[styles.item, selectedDate === item.value && styles.selectedItem]}
            onPress={() => onSelectDate(item.value)}
          >
            <Text style={[styles.day, selectedDate === item.value && styles.selectedText]}>
              {item.day}
            </Text>
            <Text style={[styles.date, selectedDate === item.value && styles.selectedText]}>
              {item.date}
            </Text>
          </Pressable>
        ))}
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { marginBottom: 20 },
  label: { fontSize: 16, fontWeight: '600', marginBottom: 10 },
  list: { flexDirection: 'row', justifyContent: 'space-between' },
  item: { alignItems: 'center', padding: 10, borderRadius: 8, backgroundColor: '#f3f4f6' },
  selectedItem: { backgroundColor: '#2563eb' },
  day: { fontSize: 12, color: '#666' },
  date: { fontSize: 14, fontWeight: '600' },
  selectedText: { color: '#fff' },
});

```

TimeSlot.js

- **Vai trò**: Hiển thị các khung giờ có sẵn để chọn
- **Nội dung**: Lưới các nút giờ; đổi màu khi được chọn
```
code
import { View, Text, Pressable, StyleSheet } from 'react-native';

export default function TimeSlot({ selectedTime, onSelectTime }) {
  const times = ['08:00', '09:00', '10:00', '14:00', '15:00', '16:00'];

  return (
    <View style={styles.container}>
      <Text style={styles.label}>Chọn giờ:</Text>
      <View style={styles.grid}>
        {times.map((time) => (
          <Pressable
            key={time}
            style={[styles.slot, selectedTime === time && styles.selectedSlot]}
            onPress={() => onSelectTime(time)}
          >
            <Text style={[styles.timeText, selectedTime === time && styles.selectedText]}>
              {time}
            </Text>
          </Pressable>
        ))}
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { marginBottom: 20 },
  label: { fontSize: 16, fontWeight: '600', marginBottom: 10 },
  grid: { flexDirection: 'row', flexWrap: 'wrap', gap: 10 },
  slot: {
    width: '30%',
    paddingVertical: 12,
    borderRadius: 8,
    backgroundColor: '#f3f4f6',
    alignItems: 'center',
  },
  selectedSlot: { backgroundColor: '#2563eb' },
  timeText: { fontSize: 14 },
  selectedText: { color: '#fff' },
});

```

BookingSummary.js

- **Vai trò**: Hiển thị tổng hợp thông tin đặt lịch
- **Nội dung**: Tên dịch vụ, ngày, giờ, khách hàng, tổng tiền
```
code
import { View, Text, StyleSheet } from 'react-native';

export default function BookingSummary({ service, date, time, customerName }) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Thông tin đặt lịch</Text>
      <View style={styles.row}>
        <Text style={styles.label}>Dịch vụ:</Text>
        <Text style={styles.value}>{service?.name}</Text>
      </View>
      <View style={styles.row}>
        <Text style={styles.label}>Thời lượng:</Text>
        <Text style={styles.value}>{service?.duration}</Text>
      </View>
      <View style={styles.row}>
        <Text style={styles.label}>Ngày:</Text>
        <Text style={styles.value}>{date}</Text>
      </View>
      <View style={styles.row}>
        <Text style={styles.label}>Giờ:</Text>
        <Text style={styles.value}>{time}</Text>
      </View>
      <View style={styles.row}>
        <Text style={styles.label}>Khách hàng:</Text>
        <Text style={styles.value}>{customerName}</Text>
      </View>
      <View style={[styles.row, styles.total]}>
        <Text style={styles.label}>Tổng tiền:</Text>
        <Text style={styles.price}>{service?.price} VNĐ</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: '#fff',
    borderRadius: 12,
    padding: 20,
    marginVertical: 15,
    borderWidth: 1,
    borderColor: '#e5e7eb',
  },
  title: { fontSize: 18, fontWeight: 'bold', marginBottom: 15, textAlign: 'center' },
  row: { flexDirection: 'row', justifyContent: 'space-between', marginBottom: 10 },
  label: { fontSize: 15, color: '#555' },
  value: { fontSize: 15, fontWeight: '500' },
  total: { marginTop: 10, paddingTop: 10, borderTopWidth: 1, borderTopColor: '#eee' },
  price: { fontSize: 16, fontWeight: 'bold', color: '#2563eb' },
});

```

HomeScreen.js
- **Vai trò**: Giao diện đầu tiên người dùng thấy
- **Nội dung**: Banner giới thiệu + danh sách tất cả dịch vụ
```
code
import { View, Text, Image, StyleSheet, ScrollView } from 'react-native';
import ServiceCard from '../components/ServiceCard';

const services = [
  {
    id: '1',
    name: 'Cắt tóc nam',
    image: 'https://images.unsplash.com/photo-1585747860147-a2a1a9a24c83?w=400',
    duration: '45 phút',
    price: 80000,
    description: 'Dịch vụ cắt tóc chuyên nghiệp, gội đầu và sấy tóc.',
  },
  {
    id: '2',
    name: 'Cắt tóc nữ',
    image: 'https://images.unsplash.com/photo-1605497788044-9e180b89b3d4?w=400',
    duration: '60 phút',
    price: 120000,
    description: 'Tư vấn kiểu tóc phù hợp với gương mặt, cắt tỉa cẩn thận.',
  },
  {
    id: '3',
    name: 'Nhuộm tóc',
    image: 'https://images.unsplash.com/photo-1522337360786-8abece9b9941?w=400',
    duration: '90 phút',
    price: 250000,
    description: 'Sử dụng thuốc nhuộm chất lượng, đa dạng màu chọn.',
  },
  {
    id: '4',
    name: 'Làm móng',
    image: 'https://images.unsplash.com/photo-1604654894876-53f8c3cd9d86?w=400',
    duration: '75 phút',
    price: 150000,
    description: 'Làm móng tay/chân, sơn móng với nhiều mẫu đẹp.',
  },
];

export default function HomeScreen({ navigation }) {
  return (
    <ScrollView style={styles.container}>
      <Image
        source={{ uri: 'https://images.unsplash.com/photo-1560066988-515c6fa54d0a?w=800' }}
        style={styles.banner}
        resizeMode="cover"
      />
      <Text style={styles.header}>Dịch vụ của chúng tôi</Text>
      {services.map((sv) => (
        <ServiceCard
          key={sv.id}
          service={sv}
          onPress={() => navigation.navigate('ServiceDetail', { service: sv })}
        />
      ))}
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, backgroundColor: '#f9fafb', padding: 16 },
  banner: { width: '100%', height: 180, borderRadius: 12, marginBottom: 20 },
  header: { fontSize: 22, fontWeight: 'bold', marginBottom: 15 },
});

```

ServiceDetailScreen.js
- **Vai trò**: Hiển thị thông tin đầy đủ của 1 dịch vụ
- **Nhận dữ liệu**: `route.params.service` nhận đối tượng dịch vụ từ màn hình trước
- **Nút hành động**: Quay lại / Đặt lịch ngay → chuyển sang màn hình đặt lịch
```
code
import { View, Text, Image, StyleSheet, Pressable } from 'react-native';

export default function ServiceDetailScreen({ route, navigation }) {
  const { service } = route.params;

  return (
    <View style={styles.container}>
      <Image source={{ uri: service.image }} style={styles.image} />
      <View style={styles.content}>
        <Text style={styles.name}>{service.name}</Text>
        <Text style={styles.duration}>⏱ Thời lượng: {service.duration}</Text>
        <Text style={styles.price}>{service.price} VNĐ</Text>
        <Text style={styles.desc}>{service.description}</Text>

        <View style={{ flexDirection: 'row', gap: 10, marginTop: 20 }}>
          <Pressable style={styles.backBtn} onPress={() => navigation.goBack()}>
            <Text style={styles.backText}>← Quay lại</Text>
          </Pressable>
          <Pressable
            style={styles.bookBtn}
            onPress={() => navigation.navigate('Booking', { service: service })}
          >
            <Text style={styles.bookText}>Đặt lịch ngay</Text>
          </Pressable>
        </View>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, backgroundColor: '#fff' },
  image: { width: '100%', height: 220 },
  content: { padding: 20 },
  name: { fontSize: 24, fontWeight: 'bold', marginBottom: 10 },
  duration: { fontSize: 16, color: '#666', marginBottom: 8 },
  price: { fontSize: 20, fontWeight: 'bold', color: '#2563eb', marginBottom: 15 },
  desc: { fontSize: 15, lineHeight: 24, color: '#444' },
  backBtn: {
    flex: 1,
    paddingVertical: 14,
    borderRadius: 8,
    borderWidth: 1,
    borderColor: '#d1d5db',
    alignItems: 'center',
  },
  backText: { fontSize: 16, color: '#4b5563' },
  bookBtn: {
    flex: 1,
    paddingVertical: 14,
    borderRadius: 8,
    backgroundColor: '#2563eb',
    alignItems: 'center',
  },
  bookText: { fontSize: 16, color: '#fff', fontWeight: '600' },
});

```

BookingScreen.js
- **Vai trò**: Thu thập thông tin lịch hẹn của người dùng
- **State quản lý**:
  - "electedDate": Ngày đã chọn
  - "selectedTime": Giờ đã chọn
  - "customerName": Tên khách hàng nhập vào
- **Kiểm tra hợp lệ**: Không để trống thông tin trước khi xác nhận
- **Chuyển dữ liệu**: Gửi toàn bộ thông tin sang màn hình xác nhận
```
code
import { View, Text, StyleSheet, Pressable, TextInput, Alert } from 'react-native';
import { useState } from 'react';
import DateSelector from '../components/DateSelector';
import TimeSlot from '../components/TimeSlot';

export default function BookingScreen({ route, navigation }) {
  const { service } = route.params;
  const [selectedDate, setSelectedDate] = useState('');
  const [selectedTime, setSelectedTime] = useState('');
  const [customerName, setCustomerName] = useState('');

  const handleConfirm = () => {
    if (!selectedDate || !selectedTime || !customerName.trim()) {
      Alert.alert('Thông báo', 'Vui lòng điền đầy đủ thông tin!');
      return;
    }
    navigation.navigate('Confirmation', {
      service,
      date: selectedDate,
      time: selectedTime,
      customerName: customerName.trim(),
    });
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Đặt lịch — {service.name}</Text>

      <DateSelector selectedDate={selectedDate} onSelectDate={setSelectedDate} />
      <TimeSlot selectedTime={selectedTime} onSelectTime={setSelectedTime} />

      <View style={styles.inputContainer}>
        <Text style={styles.label}>Tên của bạn:</Text>
        <TextInput
          style={styles.input}
          placeholder="Nhập họ và tên"
          value={customerName}
          onChangeText={setCustomerName}
        />
      </View>

      <View style={styles.btnRow}>
        <Pressable style={styles.editBtn} onPress={() => navigation.goBack()}>
          <Text style={styles.editText}>Thay đổi dịch vụ</Text>
        </Pressable>
        <Pressable style={styles.confirmBtn} onPress={handleConfirm}>
          <Text style={styles.confirmText}>Xác nhận đặt lịch</Text>
        </Pressable>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 20, backgroundColor: '#f9fafb' },
  title: { fontSize: 20, fontWeight: 'bold', marginBottom: 25, textAlign: 'center' },
  inputContainer: { marginBottom: 25 },
  label: { fontSize: 16, fontWeight: '600', marginBottom: 8 },
  input: {
    backgroundColor: '#fff',
    padding: 12,
    borderRadius: 8,
    borderWidth: 1,
    borderColor: '#d1d5db',
    fontSize: 15,
  },
  btnRow: { flexDirection: 'row', gap: 12, marginTop: 10 },
  editBtn: {
    flex: 1,
    paddingVertical: 14,
    borderRadius: 8,
    borderWidth: 1,
    borderColor: '#f59e0b',
    alignItems: 'center',
  },
  editText: { fontSize: 15, color: '#d97706' },
  confirmBtn: {
    flex: 1,
    paddingVertical: 14,
    borderRadius: 8,
    backgroundColor: '#16a34a',
    alignItems: 'center',
  },
  confirmText: { fontSize: 15, color: '#fff', fontWeight: '600' },
});

```

ConfirmationScreen.js
- **Vai trò**: Thông báo thành công và tóm tắt thông tin
- **Nhận dữ liệu**: Nhận toàn bộ thông tin đặt lịch qua "route.params"
- **Hiển thị**: Sử dụng component "BookingSummary" để tóm tắt
- **Nút hành động**: "navigation.popToTop()" → quay về Trang chủ, xóa toàn bộ lịch sử điều hướng
```
code
import { View, Text, StyleSheet, Pressable } from 'react-native';
import BookingSummary from '../components/BookingSummary';

export default function ConfirmationScreen({ route, navigation }) {
  const { service, date, time, customerName } = route.params;

  return (
    <View style={styles.container}>
      <View style={styles.iconWrap}>
        <Text style={styles.icon}>✓</Text>
      </View>
      <Text style={styles.title}>Đặt lịch thành công!</Text>
      <Text style={styles.subtitle}>Cảm ơn bạn, {customerName} 🎉</Text>

      <BookingSummary
        service={service}
        date={date}
        time={time}
        customerName={customerName}
      />

      <Pressable style={styles.homeBtn} onPress={() => navigation.popToTop()}>
        <Text style={styles.homeText}>Quay lại Trang chủ</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#f9fafb',
    alignItems: 'center',
  },
  iconWrap: {
    width: 70,
    height: 70,
    borderRadius: 35,
    backgroundColor: '#dcfce7',
    justifyContent: 'center',
    alignItems: 'center',
    marginTop: 30,
    marginBottom: 15,
  },
  icon: {
    fontSize: 36,
    color: '#16a34a',
    fontWeight: 'bold',
  },
  title: {
    fontSize: 22,
    fontWeight: 'bold',
    marginBottom: 5,
  },
  subtitle: {
    fontSize: 15,
    color: '#666',
    marginBottom: 25,
  },
  homeBtn: {
    width: '100%',
    paddingVertical: 14,
    borderRadius: 8,
    backgroundColor: '#2563eb',
    alignItems: 'center',
    marginTop: 10,
  },
  homeText: {
    fontSize: 16,
    color: '#fff',
    fontWeight: '600',
  },
});

```

KetQua:

<img width="418" height="763" alt="image" src="https://github.com/user-attachments/assets/03219b48-5b49-4879-8ec9-1843f23f62af" />

<img width="421" height="766" alt="image" src="https://github.com/user-attachments/assets/bafe3d1b-4a9c-4997-9d90-929c634466c0" />

<img width="417" height="753" alt="image" src="https://github.com/user-attachments/assets/cc9ff322-6725-429a-8514-0427daf6b76c" />

<img width="420" height="744" alt="image" src="https://github.com/user-attachments/assets/5afa298f-5852-4166-96b7-0669b15e12d5" />
