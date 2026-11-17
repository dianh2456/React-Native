Link bài nộp:
https://snack.expo.dev/@duyanhdepzai/scheduleapp

 Nội dung và chức năng từng tệp

 App.js

Nội dung: Tập hợp các thành phần của ứng dụng, khai báo trạng thái lưu ngày được chọn
Chức năng: Là tệp chính, khởi chạy ứng dụng và điều khiển luồng dữ liệu
```
code
import React, { useState } from 'react';
import { SafeAreaView, StyleSheet, StatusBar } from 'react-native';
import Header from './components/Header';
import DaySelector from './components/DaySelector';
import ScheduleList from './components/ScheduleList';
import { scheduleData, daysOfWeek } from './data/scheduleData';

const App = () => {
  const [selectedDay, setSelectedDay] = useState(daysOfWeek[0]); // Mặc định Thứ2
  const currentSchedule = scheduleData[selectedDay];

  return (
    <SafeAreaView style={styles.safeArea}>
      <StatusBar barStyle="light-content" backgroundColor="#1565C0" />
      
      <Header 
        appName="📅 ScheduleApp"
        studentName="Nguyễn Lê Duy Anh - Mã SV: CDCNTT18A03"
        className="CĐ-CNTT18A"
      />
      
      <DaySelector
        selectedDay={selectedDay}
        onSelectDay={setSelectedDay}
      />
      
      <ScheduleList
        schedule={currentSchedule}
        selectedDay={selectedDay}
      />
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  safeArea: {
    flex: 1,
    backgroundColor: '#F5F5F5',
  },
});

export default App;
```

scheduleData.js

Nội dung: Dữ liệu lịch học theo từng ngày, bao gồm thông tin môn học và màu sắc
Chức năng: Cung cấp nguồn dữ liệu cho toàn bộ ứng dụng
```
code
// Dữ liệu lịch học theo từng ngày
export const scheduleData = {
  Thứ2: [
    {
      id: 1,
      subject: "Lập trình di động",
      room: "301",
      time: "07:30 - 09:00",
      teacher: "Trần Ngọc Minh",
      color: "#4CAF50"
    },
    {
      id: 2,
      subject: "Quản trị SQL",
      room: "202",
      time: "09:15 - 10:45",
      teacher: "Nguyễn Thị Thương",
      color: "#2196F3"
    }
  ],
  Thứ3: [
    {
      id: 3,
      subject: "Cơ sở dữ liệu",
      room: "105",
      time: "07:30 - 09:00",
      teacher: "Hồ Thị Thanh Diệu",
      color: "#FF9800"
    },
    {
      id: 4,
      subject: "Tiếng Anh chuyên ngành",
      room: "401",
      time: "13:30 - 15:00",
      teacher: "Hồ Thị Thanh Tú",
      color: "#E91E63"
    }
  ],
  Thứ4: [
    {
      id: 5,
      subject: "Thiết kế giao diện",
      room: "303",
      time: "09:15 - 10:45",
      teacher: "Trần Ngọc Minh",
      color: "#9C27B0"
    }
  ],
  Thứ5: [],
  Thứ6: [
    {
      id: 6,
      subject: "Phân tích thiết kế hệ thống",
      room: "101",
      time: "07:30 - 10:45",
      teacher: "Nguyễn Thanh Hải",
      color: "#00BCD4"
    }
  ],
  Thứ7: [],
  ChủNhật: []
};

// Danh sách các ngày trong tuần
export const daysOfWeek = ["Thứ2", "Thứ3", "Thứ4", "Thứ5", "Thứ6", "Thứ7", "ChủNhật"];
```

Header.js

Nội dung: Tên ứng dụng, họ tên, mã sinh viên và lớp học
Chức năng: Hiển thị tiêu đề và thông tin ở đầu màn hình
```
code
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

const Header = ({ appName, studentName, className }) => {
  return (
    <View style={styles.headerContainer}>
      <Text style={styles.appName}>{appName}</Text>
      <Text style={styles.studentName}>👤 Sinh viên: {studentName}</Text>
      <Text style={styles.className}>📚 Lớp: {className}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  headerContainer: {
    backgroundColor: '#1976D2',
    paddingVertical: 20,
    paddingHorizontal: 15,
    alignItems: 'center',
    borderBottomLeftRadius: 20,
    borderBottomRightRadius: 20,
    elevation: 5,
  },
  appName: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#fff',
    marginBottom: 5,
  },
  studentName: {
    fontSize: 15,
    color: '#E3F2FD',
    marginBottom: 3,
  },
  className: {
    fontSize: 14,
    color: '#BBDEFB',
  },
});

export default Header;

```

DaySelector.js

Nội dung: 7 nút bấm hiển thị các ngày trong tuần
Chức năng: Cho phép người dùng chọn ngày để xem lịch học tương ứng
```
code
import React from 'react';
import { View, Text, TouchableOpacity, StyleSheet } from 'react-native';
import { daysOfWeek } from '../data/scheduleData';

const DaySelector = ({ selectedDay, onSelectDay }) => {
  return (
    <View style={styles.container}>
      {daysOfWeek.map((day) => (
        <TouchableOpacity
          key={day}
          style={[
            styles.dayButton,
            selectedDay === day && styles.selectedDay
          ]}
          onPress={() => onSelectDay(day)}
        >
          <Text
            style={[
              styles.dayText,
              selectedDay === day && styles.selectedDayText
            ]}
          >
            {day.replace('Nhật', ' CN')}
          </Text>
        </TouchableOpacity>
      ))}
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    paddingHorizontal: 10,
    paddingVertical: 15,
    backgroundColor: '#fff',
  },
  dayButton: {
    paddingVertical: 8,
    paddingHorizontal: 6,
    borderRadius: 10,
    backgroundColor: '#F5F5F5',
    minWidth: 45,
    alignItems: 'center',
  },
  selectedDay: {
    backgroundColor: '#1976D2',
  },
  dayText: {
    fontSize: 13,
    color: '#424242',
    fontWeight: '500',
  },
  selectedDayText: {
    color: '#fff',
    fontWeight: 'bold',
  },
});

export default DaySelector;

```

 ScheduleItem.js

Nội dung: Thời gian học, tên môn, phòng học và giảng viên
Chức năng: Hiển thị thông tin chi tiết của từng môn học
```
code
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

const ScheduleItem = ({ item }) => {
  return (
    <View style={[styles.card, { borderLeftColor: item.color }]}>
      <View style={styles.timeContainer}>
        <Text style={styles.timeText}>{item.time}</Text>
      </View>
      <View style={styles.infoContainer}>
        <Text style={styles.subjectText}>{item.subject}</Text>
        <Text style={styles.detailText}>📍 Phòng: {item.room}</Text>
        <Text style={styles.detailText}>👨‍🏫 Giảng viên: {item.teacher}</Text>
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  card: {
    flexDirection: 'row',
    backgroundColor: '#fff',
    marginHorizontal: 15,
    marginVertical: 8,
    borderRadius: 10,
    borderLeftWidth: 6,
    padding: 15,
    elevation: 3,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
  },
  timeContainer: {
    justifyContent: 'center',
    alignItems: 'center',
    paddingRight: 12,
    borderRightWidth: 1,
    borderRightColor: '#E0E0E0',
  },
  timeText: {
    fontSize: 13,
    fontWeight: 'bold',
    color: '#616161',
  },
  infoContainer: {
    flex: 1,
    paddingLeft: 10,
  },
  subjectText: {
    fontSize: 16,
    fontWeight: 'bold',
    color: '#212121',
    marginBottom: 5,
  },
  detailText: {
    fontSize: 14,
    color: '#616161',
    marginBottom: 2,
  },
});

export default ScheduleItem;

```

 ScheduleList.js

Nội dung: Tiêu đề ngày, danh sách môn học hoặc thông báo trống
Chức năng: Hiển thị danh sách môn học hoặc thông báo khi không có lịch học
```
code
import React from 'react';
import { View, Text, StyleSheet, ScrollView } from 'react-native';
import ScheduleItem from './ScheduleItem';

const ScheduleList = ({ schedule, selectedDay }) => {
  return (
    <View style={styles.container}>
      <Text style={styles.titleText}>📖 Lịch học - {selectedDay}</Text>
      
      {schedule.length > 0 ? (
        <ScrollView showsVerticalScrollIndicator={false}>
          {schedule.map((item) => (
            <ScheduleItem key={item.id} item={item} />
          ))}
        </ScrollView>
      ) : (
        <View style={styles.emptyContainer}>
          <Text style={styles.emojiText}>📭</Text>
          <Text style={styles.emptyText}>Không có lịch học vào ngày này!</Text>
          <Text style={styles.suggestText}>Chọn ngày khác để xem lịch học</Text>
        </View>
      )}
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F9F9F9',
    paddingTop: 15,
  },
  titleText: {
    fontSize: 18,
    fontWeight: 'bold',
    paddingHorizontal: 15,
    marginBottom: 10,
    color: '#333',
  },
  emptyContainer: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    paddingVertical: 60,
  },
  emojiText: {
    fontSize: 50,
    marginBottom: 15,
  },
  emptyText: {
    fontSize: 17,
    color: '#757575',
    fontWeight: '600',
  },
  suggestText: {
    fontSize: 14,
    color: '#9E9E9E',
    marginTop: 5,
  },
});

export default ScheduleList;
```
Ảnh kết quả :

<img width="331" height="647" alt="image" src="https://github.com/user-attachments/assets/b3da94e0-5bf0-4a84-a077-ca6392ccfb8f" />

<img width="326" height="607" alt="image" src="https://github.com/user-attachments/assets/f319142b-6fad-42a1-bc13-58ef80d5842c" />

<img width="315" height="614" alt="image" src="https://github.com/user-attachments/assets/c85bfec6-efa1-4a4d-a5d0-af56b8615f01" />




