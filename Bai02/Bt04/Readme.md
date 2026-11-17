Link bài tập:https://snack.expo.dev/@duyanhdepzai/multiscreenapp
Nội dung:

HomeScreen.js — Màn hình Trang chủ

Vai trò: Là màn hình đầu tiên người dùng thấy khi mở ứng dụng

• Hiển thị lời chào, thông tin giới thiệu

• Có nút bấm gọi hàm navigation.navigate('DanhSach') → chuyển sang màn hình Danh sách

• Luồng hoạt động: Nhấn nút → yêu cầu Stack Navigator điều hướng → mở màn hình mới
``````
code
import { View, Text, StyleSheet, TouchableOpacity } from 'react-native';

export default function HomeScreen({ navigation }) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>🏠 Trang Chủ</Text>
      <Text style={styles.subtitle}>Chào mừng bạn đến với ứng dụng!</Text>
      
      <TouchableOpacity 
        style={styles.button}
        onPress={() => navigation.navigate('DanhSach')}
      >
        <Text style={styles.buttonText}>Xem Danh Sách</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#e3f2fd',
    alignItems: 'center',
    justifyContent: 'center',
    padding: 20,
  },
  title: {
    fontSize: 28,
    fontWeight: 'bold',
    color: '#1976d2',
    marginBottom: 10,
  },
  subtitle: {
    fontSize: 16,
    color: '#555',
    marginBottom: 30,
  },
  button: {
    backgroundColor: '#1976d2',
    paddingVertical: 12,
    paddingHorizontal: 30,
    borderRadius: 8,
  },
  buttonText: {
    color: '#fff',
    fontSize: 16,
    fontWeight: '600',
  },
});

``````
Nội dung:
ListScreen.js — Màn hình Danh sách

Vai trò: Hiển thị danh sách các món ăn

• Dùng FlatList để hiển thị danh sách dài hiệu quả

• Mỗi khi nhấn vào một mục → gọi navigation.navigate('ChiTiet', { item })
→ truyền dữ liệu (thông tin món ăn) sang màn hình chi tiết

• Luồng hoạt động: Nhấn mục → đóng gói dữ liệu → gửi cho Navigator → mở màn hình Chi tiết kèm dữ liệu

```````
code

import { View, Text, StyleSheet, FlatList, TouchableOpacity } from 'react-native';

// Dữ liệu mẫu
const data = [
  { id: '1', name: 'Cà phê sữa đá', price: '22.000đ', desc: 'Cà phê pha với sữa đặc, đá viên mát lạnh' },
  { id: '2', name: 'Bún bò Huế', price: '45.000đ', desc: 'Bún với thịt bò, chả cua, nước lèo cay nồng' },
  { id: '3', name: 'Pate Cột Đèn Hải Phòng ', price: '20.000đ', desc: 'Bánh mì giòn với patê, thịt nguội, rau thơm' },
  { id: '4', name: 'Phở bò Hà Nội', price: '50.000đ', desc: 'Phở với thịt bò tái, nước dùng thanh ngọt' },
  { id: '5', name: 'Bơ già dừa non', price: '25.000đ', desc: ' Bơ chín xay mịn béo ngậy ở dưới, phủ lớp sữa dừa đánh bông mát lạnh ở trên, thêm dừa non sợi dai giòn và vụn dừa sấy.' },
];

export default function ListScreen({ navigation }) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>📋 Danh sách món ăn</Text>
      
      <FlatList
        data={data}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <TouchableOpacity
            style={styles.item}
            onPress={() => navigation.navigate('ChiTiet', { item })}
          >
            <Text style={styles.itemName}>{item.name}</Text>
            <Text style={styles.itemPrice}>{item.price}</Text>
          </TouchableOpacity>
        )}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff8e1',
    padding: 15,
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#e65100',
    marginBottom: 15,
    textAlign: 'center',
  },
  item: {
    backgroundColor: '#fff',
    padding: 15,
    marginBottom: 10,
    borderRadius: 8,
    borderWidth: 1,
    borderColor: '#ffcc80',
  },
  itemName: {
    fontSize: 18,
    fontWeight: '600',
    color: '#333',
  },
  itemPrice: {
    fontSize: 14,
    color: '#e65100',
    marginTop: 5,
  },
});
````````
Nội dung
DetailScreen.js — Màn hình Chi tiết

Vai trò: Hiển thị thông tin chi tiết của món ăn được chọn

• Dùng route.params.item → nhận dữ liệu được gửi từ màn hình Danh sách

• Nút quay lại gọi navigation.goBack() → quay về màn hình trước đó

• Luồng hoạt động: Nhận dữ liệu → hiển thị ra giao diện → nhấn quay lại → đóng màn hình hiện tại → quay về Danh sách

`````
code
import { View, Text, StyleSheet, TouchableOpacity } from 'react-native';
import { Ionicons } from '@expo/vector-icons';

export default function DetailScreen({ route, navigation }) {
  const { item } = route.params; // Nhận dữ liệu từ ListScreen

  return (
    <View style={styles.container}>
      {/* Nút quay lại */}
      <TouchableOpacity style={styles.backButton} onPress={() => navigation.goBack()}>
        <Ionicons name="arrow-back" size={24} color="#fff" />
      </TouchableOpacity>

      <View style={styles.card}>
        <Text style={styles.name}>{item.name}</Text>
        <Text style={styles.price}>💰 Giá: {item.price}</Text>
        <Text style={styles.desc}>📝 Mô tả: {item.desc}</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#e8f5e9',
    padding: 20,
  },
  backButton: {
    backgroundColor: '#4caf50',
    width: 44,
    height: 44,
    borderRadius: 22,
    alignItems: 'center',
    justifyContent: 'center',
    marginBottom: 20,
  },
  card: {
    backgroundColor: '#fff',
    padding: 25,
    borderRadius: 12,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
    elevation: 3,
  },
  name: {
    fontSize: 26,
    fontWeight: 'bold',
    color: '#2e7d32',
    marginBottom: 15,
  },
  price: {
    fontSize: 18,
    color: '#e64a19',
    marginBottom: 15,
  },
  desc: {
    fontSize: 16,
    color: '#555',
    lineHeight: 24,
  },
});
``````
Nội dung:
ProfileScreen.js — Màn hình Cá nhân

Vai trò: Hiển thị thông tin cá nhân người dùng

• Đơn giản hiển thị thông tin tĩnh

• Được quản lý bởi Tab Navigator ở dưới cùng

`````
code
import { View, Text, StyleSheet } from 'react-native';

export default function ProfileScreen() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>👤 Thông tin cá nhân</Text>
      <Text style={styles.info}>Họ tên: Nguyễn Lê Duy Anh</Text>
      <Text style={styles.info}>Mã SV: CDCNTT18A03</Text>
      <Text style={styles.info}>Lớp: CĐ-CNTT18A</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f3e5f5',
    alignItems: 'center',
    justifyContent: 'center',
    padding: 20,
  },
  title: {
    fontSize: 26,
    fontWeight: 'bold',
    color: '#7b1fa2',
    marginBottom: 30,
  },
  info: {
    fontSize: 18,
    color: '#555',
    marginBottom: 10,
  },
});
```````
Kết quả hiển thị :

<img width="321" height="617" alt="image" src="https://github.com/user-attachments/assets/931082ff-d7bc-4ed6-9edd-22a9c2fc02a5" />

<img width="333" height="616" alt="image" src="https://github.com/user-attachments/assets/e486a85d-9df6-4d42-941f-3788ec7ae4e3" />

<img width="332" height="623" alt="image" src="https://github.com/user-attachments/assets/ce41c1aa-df28-416e-9298-dbe708341370" />




