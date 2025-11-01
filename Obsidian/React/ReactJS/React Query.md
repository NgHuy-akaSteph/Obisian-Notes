## 1. useQuery
- `useQuery`: là hook để lấy dữ liệu (fetch).
- Các thuộc tính của useQuery:
	- `queryKey(Array | string)`: giá trị duy nhất để react nhận diện  và cache kết quả.
	- `queryFn(() => Promise<T>)`: hàm async để fetch dữ liệu.
	- `retry(number|boolean)`: 1,2...: số lần thử lại, false: không cho thử lại
	- `select(data => any)`: cho phép biến đổi dữ liệu trước khi trả về (giống map)
	- `enabled(boolean)`: nếu false -> query không tự chạy được
	- `keepPreviousData (boolean)`: giữ lại dữ liệu cũ trong khi đang fetch dữ liệu mới => dùng cho phân trang
- ==Notes==: `!!`: chuyển một giá trị bất kỳ thành boolean.
## 2. useMutation
* `useMutation`: là hook dùng để thực hiện những thao tác thay đổi dữ liệu (POST, PUT, PATCH, DELETE)
* Các tham số liên quan:
	- `mutate()`: hàm thực thi mutation 
	- `mutateAsync()`: giống mutatte
	- `data`: kết quả trả về
	- `error`: lỗi (nếu thất bại)
	- `isPending/isLoading`: mutation đang chạy
	- `isError`: có lỗi
	- `isSuccess`: Thành công
	- `reset()`: reset lại trạng thái mutation
	- `onSuccess()`: thực hiện khi mutation thành công
	- `onError()`: khi mutation thất bại
	- `onSettled()`: khi mutation kết thúc (thành công/thất bại) -> reset form, ẩn loading, log kết quả

[[React Form Hook & Zod]]


