App.js


```
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
