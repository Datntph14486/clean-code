# 💡 Bạn của 6 tháng sau sẽ cảm ơn bạn nếu bạn áp dụng Clean Code!

# 1️. Đặt tên biến, hàm, class rõ ràng, có ý nghĩa

    ❌ Bad:
    	let d = new Date();

    ✅ Good:
    	let currentDate = new Date();

# 2. Tránh viết code thừa, dư thừa logic

    ❌ Bad:
    	if (isLoggedIn === true) {
    		return true;
    	} else {
    		return false;
    	};

    ✅ Good:
    	return isLoggedIn;

# 3. Một hàm chỉ nên làm một việc duy nhất (Nguyên tắc Single Responsibility)

    ❌ Bad - Một hàm làm quá nhiều việc
     - Hàm này vừa lấy dữ liệu, vừa xử lý logic, vừa in kết quả:

    	function processUser(userId) {
    		// Lấy dữ liệu user từ database
    		const user = database.getUserById(userId);

    		// Kiểm tra user có quyền admin không
    		const isAdmin = user.role === "admin";

    		// In kết quả ra màn hình
    		console.log(`User ${user.name} is ${isAdmin ? "an Admin" : "not an Admin"}`);
    	};

    ✅ Good - Mỗi hàm chỉ làm một việc
     - Tách ra thành 3 hàm nhỏ để dễ bảo trì:
     
    	function getUserById(userId) {
    		return database.getUserById(userId);
    	}

    	function checkIfAdmin(user) {
    		return user.role === "admin";
    	}

    	function printUserRole(user) {
    		const isAdmin = checkIfAdmin(user);
    		console.log(`User ${user.name} is ${isAdmin ? "an Admin" : "not an Admin"}`);
    	}

    	// Sử dụng
    	const user = getUserById(1);
    	printUserRole(user);

# 4. Không viết lại những logic giống nhau - Tránh code lặp (Don’t Repeat Yourself - DRY)

    - Giả sử bạn có một ứng dụng tính giá sau thuế cho nhiều loại sản phẩm:
    
    ❌ Bad (Code bị lặp lại nhiều lần):
    	function calculatePriceForBook(price) {
    		return price + price * 0.1; // Thuế 10%
    	}

    	function calculatePriceForElectronics(price) {
    		return price + price * 0.2; // Thuế 20%
    	}

    	function calculatePriceForClothes(price) {
    		return price + price * 0.15; // Thuế 15%
    	}

    ✅ Good (Áp dụng DRY, tái sử dụng hàm chung):
    	function calculatePrice(price, taxRate) {
    		return price + price * taxRate;
    	}

    	// Sử dụng
    	const bookPrice = calculatePrice(100, 0.1);
    	const electronicsPrice = calculatePrice(100, 0.2);
    	const clothesPrice = calculatePrice(100, 0.15);

# 5. Viết code dễ đọc hơn là tối ưu hóa quá mức

    - Đừng cố tối ưu hóa code quá sớm. Hãy viết code rõ ràng, dễ hiểu trước, rồi mới tối ưu khi thực sự cần thiết.

    ❌ Bad:
    	function f(arr) {
    		return arr.reduce((a, b) => a + (b % 2 ? 0 : b), 0);
    	}

    ✅ Good (Viết code dễ đọc hơn):
    	function sumEvenNumbers(numbers) {
    		return numbers
    			.filter(num => num % 2 === 0) // Lọc ra số chẵn
    			.reduce((sum, num) => sum + num, 0); // Cộng dồn các số chẵn
    	}

# 6. Tránh điều kiện lồng nhau quá sâu (Avoid Deep Nesting)

    - Các điều kiện lồng nhau quá sâu (nested if statements) làm code khó đọc, khó hiểu và khó bảo trì. Hãy tìm cách đơn giản hóa chúng.

    ❌ Bad:
    	function processOrder(order) {
    		if (order) {
    			if (order.status === "pending") {
    				if (order.items.length > 0) {
    					if (order.paymentSuccess) {
    						console.log("Đơn hàng đang xử lý.");
    					} else {
    						console.log("Thanh toán thất bại.");
    					}
    				} else {
    					console.log("Đơn hàng không có sản phẩm.");
    				}
    			} else {
    				console.log("Đơn hàng không ở trạng thái chờ xử lý.");
    			}
    		} else {
    			console.log("Đơn hàng không hợp lệ.");
    		}
    	}

    ✅ Good:
    	function processOrder(order) {
    		if (!order) {
    			console.log("Đơn hàng không hợp lệ.");
    			return;
    		}

    		if (order.status !== "pending") {
    			console.log("Đơn hàng không ở trạng thái chờ xử lý.");
    			return;
    		}

    		if (order.items.length === 0) {
    			console.log("Đơn hàng không có sản phẩm.");
    			return;
    		}

    		if (!order.paymentSuccess) {
    			console.log("Thanh toán thất bại.");
    			return;
    		}

    		console.log("Đơn hàng đang xử lý.");
    	};
# 7. Giữ cấu trúc code nhất quán (Consistent Structure)
    - Thống nhất cách đặt tên, format, vị trí các hàm để dễ đọc.
    - Tuân theo một coding style duy nhất trong dự án.
