Yêu cầu 1: Tạo một collection tên là products và chèn vào 3 sản phẩm với các field: name, price, category sử dụng db.products.insertMany()

db.products.insertMany([
{ name: "Laptop", price: 1200, category: "Electronics" },
{ name: "Shirt", price: 30, category: "Clothing" },
{ name: "Book", price: 15, category: "Education" }
])

Yêu cầu 2: Tạo một collection orders với dữ liệu chứa các trường: orderId, customerName, orderDate, totalAmount. Thêm ít nhất 2 đơn hàng. Sử dụng

insertOne() hoặc insertMany().
db.orders.insertMany([
{
orderId: "ORD001",
customerName: "Nguyen Van A",
orderDate: new Date("2025-08-01"),
totalAmount: 1500
},
{
orderId: "ORD002",
customerName: "Tran Thi B",
orderDate: new Date("2025-08-02"),
totalAmount: 300
}
])

Yêu cầu 3: Insert 5 documents vào collection users với các field: name, email, age sử dụng insertMany()

db.users.insertMany([
{ name: "Alice", email: "alice@example.com", age: 25 },
{ name: "Bob", email: "bob@example.com", age: 19 },
{ name: "Charlie", email: "charlie@example.com", age: 35 },
{ name: "David", email: "david@example.com", age: 28 },
{ name: "Eva", email: "eva@example.com", age: 42 }
])

Yêu cầu 4: Tìm tất cả các user có độ tuổi lớn hơn 25 và chỉ hiển thị name, email với find() và projection.

db.users.find(
{ age: { $gt: 25 } },
{ \_id: 0, name: 1, email: 1 }
)

Yêu cầu 5: Cập nhật tuổi của user tên “Alice” thành 31.

db.users.updateOne(
{ name: "Alice" },
{ $set: { age: 31 } }
)

Yêu cầu 6: Xóa tất cả user có tuổi nhỏ hơn 20.

db.users.deleteMany(
{ age: { $lt: 20 } }
)

Yêu cầu 7: Tìm 3 người lớn tuổi nhất trong bảng users.

db.users.find().sort({ age: -1 }).limit(3)

Yêu cầu 8: Tìm 3 user có tuổi cao nhất và hiển thị name, age sử dụng sort() + limit() + projection.

db.users.find(
{},
{ \_id: 0, name: 1, age: 1 }
).sort({ age: -1 }).limit(3)

Yêu cầu 9: Thực hiện truy vấn aggregation để đếm số lượng user theo từng độ tuổi với $group.

db.users.aggregate([
{
$group: {
_id: "$age",
count: { $sum: 1 }
}
}
])

Yêu cầu 10: Tính tuổi trung bình của user có tuổi từ 25 trở lên bằng aggregation pipeline (kết hợp $match và $group)

db.users.aggregate([
{ $match: { age: { $gte: 25 } } },
{
$group: {
_id: null,
averageAge: { $avg: "$age" }
}
}
])
