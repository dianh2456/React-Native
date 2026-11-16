Link bài tập:
https://snack.expo.dev/@duyanhdepzai/-learningapp

App.js

Vai trò: Tệp chính của ứng dụng, là điểm khởi đầu khi ứng dụng chạy.

Nội dung & Chức năng:

• Khai báo các thư viện cần sử dụng

• Nhập (import) các component con: Header, StatCard, CourseCard, BottomMenu

• Xây dựng cấu trúc giao diện tổng thể của trang Home

• Sắp xếp vị trí hiển thị các component theo thứ tự: Lời chào → Thống kê → Danh sách môn học → Thanh menu dưới

• Định dạng kiểu chữ, màu sắc, kích thước cho toàn bộ giao diện

```
code

import { View, Text, StyleSheet, ScrollView } from 'react-native';

function Header() {
  return (
    <View style={styles.header}>
      <Text style={styles.hello}>👋 Xin chào, Nguyễn Lê Duy Anh!</Text>
      <Text style={styles.info}>Mã SV: CD-CNTT18A03 | Lớp: CD-CNTT18A</Text>
    </View>
  );
}

function StatCard({ so, ten, mau }) {
  return (
    <View style={[styles.statBox, { backgroundColor: mau }]}>
      <Text style={styles.statSo}>{so}</Text>
      <Text style={styles.statTen}>{ten}</Text>
    </View>
  );
}

function CourseCard({ ten, gv, tinchi }) {
  return (
    <View style={styles.courseBox}>
      <Text style={styles.courseTen}>{ten}</Text>
      <Text>GV: {gv} | {tinchi} tín chỉ</Text>
    </View>
  );
}

function BottomMenu() {
  return (
    <View style={styles.menu}>
      <Text style={styles.menuItem}>🏠 Trang chủ</Text>
      <Text style={styles.menuItem}>📚 Môn học</Text>
      <Text style={styles.menuItem}>👤 Cá nhân</Text>
    </View>
  );
}

export default function App() {
  return (
    <View style={styles.container}>
      <Header />
      <ScrollView style={styles.body}>
        <Text style={styles.tieude}>📊 Thống kê</Text>
        <View style={styles.statRow}>
          <StatCard so="6" ten="Đang học" mau="#bbdefb" />
          <StatCard so="12" ten="Hoàn thành" mau="#c8e6c9" />
          <StatCard so="54" ten="Tín chỉ" mau="#fff9c4" />
        </View>
        <Text style={styles.tieude}>📖 Môn học</Text>
        <CourseCard ten="Lập trình di động" gv="Thầy Trần Ngọc Minh" tinchi="3" />
        <CourseCard ten="Lập trình Web" gv="Cô Thương Nguyễn" tinchi="3" />
        <CourseCard ten="Cơ sở dữ liệu" gv="Thầy Nguyễn Thanh Hải" tinchi="4" />
      </ScrollView>
      <BottomMenu />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f5f5',
  },
  header: {
    backgroundColor: '#2196F3',
    paddingTop: 50,
    paddingBottom: 25,
    paddingHorizontal: 20,
  },
  hello: {
    fontSize: 22,
    fontWeight: 'bold',
    color: '#fff',
  },
  info: {
    fontSize: 14,
    color: '#e3f2fd',
    marginTop: 5,
  },
  body: {
    flex: 1,
    padding: 15,
  },
  tieude: {
    fontSize: 18,
    fontWeight: 'bold',
    marginTop: 5,
    marginBottom: 10,
  },
  statRow: {
    flexDirection: 'row',
    gap: 8,
    marginBottom: 20,
  },
  statBox: {
    flex: 1,
    padding: 12,
    borderRadius: 10,
    alignItems: 'center',
  },
  statSo: {
    fontSize: 20,
    fontWeight: 'bold',
  },
  statTen: {
    fontSize: 11,
    marginTop: 3,
  },
  courseBox: {
    backgroundColor: '#fff',
    padding: 15,
    borderRadius: 10,
    marginBottom: 10,
  },
  courseTen: {
    fontSize: 15,
    fontWeight: 'bold',
    marginBottom: 5,
  },
  menu: {
    flexDirection: 'row',
    backgroundColor: '#fff',
    borderTopWidth: 1,
    borderTopColor: '#ddd',
    paddingVertical: 12,
    paddingBottom: 20,
  },
  menuItem: {
    flex: 1,
    textAlign: 'center',
    fontSize: 12,
  },
});
```
Header.js

Vai trò: Component hiển thị phần đầu trang.

Nội dung & Chức năng:

• Hiển thị lời chào cá nhân hóa: "👋 Xin chào, Nguyễn Lê Duy Anh!"

• Hiển thị thông tin sinh viên: Mã sinh viên và Lớp

• Thiết kế giao diện với nền màu xanh dương, chữ trắng nổi bật

• Tạo góc bo tròn ở phía dưới để giao diện mềm mại hơn

```
code

import { View, Text, StyleSheet } from 'react-native';

export default function Header() {
  return (
    <View style={styles.header}>
      <Text style={styles.greeting}>👋 Xin chào, Nguyễn Lê Duy Anh!</Text>
      <Text style={styles.info}>Mã SV: CD-CNTT18A03 | Lớp: CD-CNTT18A</Text>
      <Text style={styles.date}>Ngày: 24/05/2006</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  header: {
    backgroundColor: '#2196F3',
    padding: 20,
    paddingTop: 40,
    borderBottomLeftRadius: 20,
    borderBottomRightRadius: 20,
  },
  greeting: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#fff',
    marginBottom: 5,
  },
  info: {
    fontSize: 14,
    color: '#E3F2FD',
    marginBottom: 3,
  },
  date: {
    fontSize: 12,
    color: '#BBDEFB',
  },
});

```
StatCard.js

Vai trò: Component hiển thị từng khối số liệu thống kê.

Nội dung & Chức năng:

• Nhận dữ liệu từ App.js: giá trị số, tên chỉ tiêu, màu nền

• Hiển thị số liệu thống kê: Số môn đang học, số môn đã hoàn thành, tổng số tín chỉ

• Thiết kế khối vuông bo góc, hiển thị số lớn và mô tả nhỏ bên dưới

• Sử dụng màu nền khác nhau cho từng chỉ tiêu để dễ phân biệt

```
code
import { View, Text, StyleSheet } from 'react-native';

export default function StatCard({ title, value, icon, color }) {
  return (
    <View style={[styles.card, { backgroundColor: color || '#fff' }]}>
      <Text style={styles.icon}>{icon}</Text>
      <Text style={styles.value}>{value}</Text>
      <Text style={styles.title}>{title}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  card: {
    flex: 1,
    borderRadius: 12,
    padding: 15,
    alignItems: 'center',
    justifyContent: 'center',
    margin: 5,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
    elevation: 3,
  },
  icon: {
    fontSize: 24,
    marginBottom: 5,
  },
  value: {
    fontSize: 22,
    fontWeight: 'bold',
    color: '#333',
  },
  title: {
    fontSize: 11,
    color: '#666',
    textAlign: 'center',
    marginTop: 3,
  },
});
```
CourseCard.js
Vai trò: Component hiển thị từng khối số liệu thống kê.

Nội dung & Chức năng:

• Nhận dữ liệu từ App.js: giá trị số, tên chỉ tiêu, màu nền

• Hiển thị số liệu thống kê: Số môn đang học, số môn đã hoàn thành, tổng số tín chỉ

• Thiết kế khối vuông bo góc, hiển thị số lớn và mô tả nhỏ bên dưới

• Sử dụng màu nền khác nhau cho từng chỉ tiêu để dễ phân biệt

```
code

import { View, Text, StyleSheet } from 'react-native';

export default function CourseCard({ name, teacher, credits, progress }) {
  return (
    <View style={styles.card}>
      <View style={styles.headerRow}>
        <Text style={styles.courseName}>{name}</Text>
        <Text style={styles.credits}>{credits} TC</Text>
      </View>
      <Text style={styles.teacher}>Giảng viên: {teacher}</Text>
      <View style={styles.progressBarBg}>
        <View style={[styles.progressBarFill, { width: `${progress}%` }]} />
      </View>
      <Text style={styles.progressText}>Tiến độ: {progress}%</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  card: {
    backgroundColor: '#fff',
    borderRadius: 12,
    padding: 15,
    marginBottom: 12,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 1 },
    shadowOpacity: 0.08,
    shadowRadius: 3,
    elevation: 2,
  },
  headerRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 6,
  },
  courseName: {
    fontSize: 16,
    fontWeight: 'bold',
    color: '#333',
  },
  credits: {
    fontSize: 13,
    color: '#2196F3',
    fontWeight: '600',
  },
  teacher: {
    fontSize: 13,
    color: '#666',
    marginBottom: 10,
  },
  progressBarBg: {
    height: 6,
    backgroundColor: '#E0E0E0',
    borderRadius: 3,
    overflow: 'hidden',
  },
  progressBarFill: {
    height: '100%',
    backgroundColor: '#4CAF50',
    borderRadius: 3,
  },
  progressText: {
    fontSize: 11,
    color: '#888',
    marginTop: 4,
  },
});
````
BottomMenu.js
Vai trò: Component hiển thị thông tin từng môn học.

Nội dung & Chức năng:

• Nhận thông tin môn học: Tên môn, tên giảng viên, số tín chỉ

• Hiển thị dưới dạng thẻ riêng cho từng môn

• Phân cấp thông tin: Tên môn in đậm, thông tin phụ nhỏ hơn

• Nền trắng với viền nhẹ tạo sự rõ ràng, dễ đọc danh sách
```
code

import { View, Text, StyleSheet, TouchableOpacity } from 'react-native';

export default function BottomMenu() {
  const menuItems = [
    { icon: '🏠', label: 'Trang chủ', active: true },
    { icon: '📚', label: 'Môn học', active: false },
    { icon: '📊', label: 'Điểm số', active: false },
    { icon: '👤', label: 'Hồ sơ', active: false },
  ];

  return (
    <View style={styles.menu}>
      {menuItems.map((item, index) => (
        <TouchableOpacity key={index} style={styles.menuItem}>
          <Text style={styles.icon}>{item.icon}</Text>
          <Text style={[styles.label, item.active && styles.activeLabel]}>
            {item.label}
          </Text>
        </TouchableOpacity>
      ))}
    </View>
  );
}

const styles = StyleSheet.create({
  menu: {
    flexDirection: 'row',
    backgroundColor: '#fff',
    borderTopWidth: 1,
    borderTopColor: '#E0E0E0',
    paddingVertical: 8,
    paddingBottom: 20,
  },
  menuItem: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  icon: {
    fontSize: 20,
    marginBottom: 2,
  },
  label: {
    fontSize: 10,
    color: '#757575',
  },
  activeLabel: {
    color: '#2196F3',
    fontWeight: '600',
  },
});
````
Kết quả sau cùng
<img width="336" height="657" alt="image" src="https://github.com/user-attachments/assets/b3a1151f-23b4-447b-97fc-08fe775e23c7" />


