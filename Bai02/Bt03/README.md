Link bài:https://snack.expo.dev/@duyanhdepzai/productapp


File: App.js

 Nội dung:

• Khai báo mảng productList chứa thông tin 6 sản phẩm (tên, ảnh, giá, mô tả)

• Import component ProductCard để sử dụng

• Sử dụng FlatList để duyệt mảng và hiển thị danh sách sản phẩm

• Bố cục tiêu đề trang + danh sách sản phẩm

• Định dạng giao diện chính

 Vai trò:

• Quản lý dữ liệu: Nơi khai báo và lưu trữ danh sách sản phẩm

• Điều phối: Truyền dữ liệu cho ProductCard thông qua props

• Hiển thị: Dùng FlatList render ra toàn bộ danh sách một cách mượt mà

• Là điểm bắt đầu của ứng dụng

````````
code
import React from 'react';
import { View, Text, FlatList, StyleSheet, SafeAreaView } from 'react-native';
import ProductCard from './components/ProductCard';


const productList = [
  {
    id: '1',
    name: 'MacBook Air M3 13 inch',
    image: 'https://images.unsplash.com/photo-1517336714731-489689fd1ca8?w=400&h=400&fit=crop',
    price: '32.990.000',
    description: 'Chip Apple M3, 8GB RAM, 256GB SSD, màn hình Retina',
  },
  {
    id: '2',
    name: 'iPhone 16 Pro Max 2TB',
    image: 'https://images.unsplash.com/photo-1592750475338-74b7b21085ab?w=400&h=400&fit=crop',
    price: '46.490.000',
    description: 'Titan, chip A18 Pro, camera 48MP, màn hình 6.9 inch',
  },
  {
    id: '3',
    name: 'Tai nghe AirPods Pro 2',
    image: 'https://images.unsplash.com/photo-1600294037681-c80b4cb5b434?w=400&h=400&fit=crop',
    price: '5.690.000',
    description: 'Chống ồn chủ động, âm thanh không gian, sạc USB-C',
  },
  {
    id: '4',
    name: 'iPad Air M2 11 inch',
    image: 'https://images.unsplash.com/photo-1544244015-0df4b3ffc6b0?w=400&h=400&fit=crop',
    price: '17.990.000',
    description: 'Chip M2, màn hình Liquid Retina, hỗ trợ Apple Pencil Pro',
  },
  {
    id: '5',
    name: 'Apple Watch Series 10',
    image: 'https://images.unsplash.com/photo-1546868871-7041f2a55e12?w=400&h=400&fit=crop',
    price: '11.490.000',
    description: 'Màn hình lớn hơn, phát hiện độ sâu, vỏ nhôm',
  },
  {
    id: '6',
    name: 'Bàn phím Magic Keyboard',
    image: 'https://images.unsplash.com/photo-1587829741301-dc798b83cf39?w=400&h=400&fit=crop',
    price: '3.290.000',
    description: 'Kết nối Bluetooth, pin sạc dùng được 1 tháng',
  },
];

export default function App() {
  return (
    <SafeAreaView style={styles.safeArea}>
      <View style={styles.container}>
        <Text style={styles.pageTitle}>🛒DUY ANH APPLE🍎</Text>
        <Text style={styles.pageSubtitle}>Danh sách sản phẩm nổi bật</Text>
        
        <FlatList
          data={productList}
          keyExtractor={(item) => item.id}
          showsVerticalScrollIndicator={false}
          contentContainerStyle={{ paddingBottom: 20 }}
          renderItem={({ item }) => (
            <ProductCard
              name={item.name}
              image={item.image}
              price={item.price}
              description={item.description}
            />
          )}
        />
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeAreaView: {
    flex: 1,
    backgroundColor: '#F5F5F7',
  },
  container: {
    flex: 1,
    backgroundColor: '#F5F5F7',
    paddingTop: 16,
  },
  pageTitle: {
    fontSize: 22,
    fontWeight: 'bold',
    textAlign: 'center',
    color: '#1D1D1F',
  },
  pageSubtitle: {
    fontSize: 14,
    textAlign: 'center',
    color: '#86868B',
    marginTop: 4,
    marginBottom: 12,
    },
});

````````
File: components/ProductCard.js

 Nội dung:

• Khai báo component ProductCard nhận vào 4 tham số: name, image, price, description

• Sử dụng các thành phần cơ bản: View, Text, Image để bố cục giao diện 1 thẻ sản phẩm

• Định dạng giao diện bằng StyleSheet: kích thước, màu sắc, bóng, viền...

 Vai trò:

• Tái sử dụng: Viết 1 lần dùng cho tất cả sản phẩm

• Tách biệt: Chỉ chịu trách nhiệm hiển thị thông tin 1 sản phẩm

• Nhận dữ liệu từ bên ngoài thông qua props → linh hoạt, dễ quản lý

``````````
code
import React from 'react';
import { View, Text, Image, StyleSheet } from 'react-native';

const ProductCard = ({ name, image, price, description }) => {
  return (
    <View style={styles.card}>
      <Image 
        source={{ uri: image }} 
        style={styles.productImage}
        resizeMode="cover"
      />
      <View style={styles.infoContainer}>
        <Text style={styles.productName} numberOfLines={2}>{name}</Text>
        <Text style={styles.productPrice}>{price} VNĐ</Text>
        <Text style={styles.productDescription} numberOfLines={2}>{description}</Text>
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  card: {
    flexDirection: 'row',
    backgroundColor: '#FFFFFF',
    borderRadius: 12,
    padding: 12,
    marginVertical: 8,
    marginHorizontal: 16,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 6,
    elevation: 4,
  },
  productImage: {
    width: 90,
    height: 90,
    borderRadius: 8,
  },
  infoContainer: {
    flex: 1,
    marginLeft: 12,
    justifyContent: 'center',
  },
  productName: {
    fontSize: 15,
    fontWeight: '700',
    color: '#1A1A1A',
  },
  productPrice: {
    fontSize: 14,
    fontWeight: '600',
    color: '#E53935',
    marginTop: 4,
  },
  productDescription: {
    fontSize: 12,
    color: '#707070',
    marginTop: 4,
  },
});

export default ProductCard;

```````````

Hình ảnh kết quả :
<img width="336" height="614" alt="image" src="https://github.com/user-attachments/assets/e1c7caab-cf9a-4a2f-95f1-8a35bc4956ef" />
