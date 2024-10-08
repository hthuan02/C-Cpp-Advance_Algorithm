<details>
  <summary> **BÀI 10: LIKED LIST**</summary>


- Liked list (danh sách liên kết): Là cấu trúc dữ liệu gồm chuổi các node(nút) liên kết với nhau, mỗi node gồm 2 thành phần: Data và con trỏ (*Next).

  _VD0:_ Cho mảng `int array[] = {2,7,4,5,3};`

- Dùng Malloc:
  
        // Malloc(); //Lưu trữ 5 phần tử * sizeof(int)= (20byte)

        // Free():

        // Thêm - Thu hồi phần tử bằng cách thủ công, nhưng đối với array[10000] thì không thể làm thủ công được.

  ➡️➡️➡️➡️➡️
- Liked list: Tạo 5 node

    <img src="https://github.com/hthuan02/C_Cpp_Advance/blob/main/Bai10_Linked-List/liked_list.png" alt="Memory Layout" width="800"/>

    - Trong danh sách liên kết này có thể thêm hoặc thu hồi tùy ý các phần tử.
 
    - Liked LIST còn có thể sử dụng ở quy mô lớn hơn như array[10000].
 
    - Các hàm sử dụng của danh sách dữ liệu LIST:

    ```
        node *createNode(int value); //Tạo 1 node mới, có giá trị value và trả về con trỏ node
        void push_back(node** array, int value); //Thêm 1 node mới có giá trị value vào cuối danh sách 
        void push_front(node **array, int value); //Thêm 1 node có giá trị value đầu danh sách
        void pop_back(node **array); //Xóa node cuối danh sách 
        void pop_front(node **array); //Xóa node đầu danh sách 
        int front(node *array); //Lấy giá trị của node đầu tiên
        int back(node *array); //Lấy giá trị của node cuối cùng
        void insert(node **array, int value, int pos); //Thêm 1 node vào một vị trí bất kỳ(int pos là vị trí)
        void delete_list(node **array, int pos); //Xóa 1 node ở vị trí bất kỳ
        int size(node *array); //Lấy kích thước node của danh sách
        int get(node *array, int pos); //Lấy giá trị của node(tại pos) của danh sách

        bool empty(node *array); // kiem tra list co rong hay khong
        //Không có hàm kiểm tra đầy, vì nó k quan tâm đến số lượng
    ```

**Ứng dụng: Liked List giúp quản lý danh sách tốt hơn mảng.**

# Các hàm thường sử dụng trong danh sách liên kết(Liked List)

## 1. Hàm thêm 1 node ở cuối LIST
```
void push_back(Node **array, int value)
{
    Node *temp = createNode(value);

    if (*array == NULL)
    {
        temp = *array;
    }

    else
    {
        Node *p;
        while (p->next != NULL)
        {
            p = p->next;
        }
        p->next = temp;
    }
}
```
## 2. Hàm xóa 1 node ở cuối LIST
```
void pop_back(Node **array)
{
    Node *p = *array;
    Node *temp;
    int i = 0;

    while (p->next != NULL)
    {
        p = p->next;
        i++;
    }
    free(p);

    int j;
    temp = *array;
    for (j = 0; j < i - 1; j++)
    {
        temp = temp->next;
    }
    temp->next = NULL;
}
```
## 3. Hàm thêm 1 node ở đầu LIST
```
void push_front(Node **array, int value)
{
    Node *new_node = createNode(value);

    new_node->next = *array;
    *array = new_node;
}
## 4. Hàm xóa 1 node ở đầu LIST
void pop_front(Node **array)
{
    if (*array == NULL)
    {
        return;
    }
    Node *temp = *array;
    *array = (*array)->next;
    free(temp);
}
```
## 5. Hàm thêm 1 node vị trí bất kỳ trong LIST
```
void insert(Node **array, int value, int pos)
{
    Node *new_node = createNode(value);
    Node *p = *array;
    int index = 0;

    while (p->next != NULL && index != pos - 1)
    {
        p = p->next;
        index++;
    }

    if (index == pos - 1)
    {
        new_node->next = (p->next);
        p->next = new_node;
    }
}
```
## 6. Hàm xóa 1 node vị trí bất kỳ trong LIST
```
void delete_list(Node **array, int pos)
{
    // Con trỏ tạm để thao tác với danh sách
    Node *p = *array;

    // Nếu danh sách trống thì không làm gì và thoát
    if (*array == NULL)
        return;

    // Xóa node đầu tiên (vị trí pos = 0)
    if (pos == 0)
    {
        *array = p->next;
        free(p);
        return;
    }

    // Duyệt qua danh sách để tìm node đứng trước vị trí cần xóa
    int i;
    for (i = 0; p != NULL && i < pos - 1; i++)
    {
        p = p->next; // Tiến tới node tiếp theo
    }

    // Kiểm tra nếu vị trí cần xóa không hợp lệ (vượt quá chiều dài danh sách)
    if (p == NULL || p->next == NULL)
        return;

    // Tìm được node cần xóa
    Node *temp = p->next; // Node tại vị trí cần xóa
    p->next = temp->next; // Cập nhật liên kết để bỏ qua node cần xóa

    // Giải phóng bộ nhớ của node cần xóa
    free(temp);
}
```








    
