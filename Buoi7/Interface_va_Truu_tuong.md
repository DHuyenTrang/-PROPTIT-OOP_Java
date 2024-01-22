**INTERFACE VÀ TRỪU TƯỢNG**

- [I. Interface là gì?](#i-interface-là-gì)
- [II. Abstract Class](#ii-abstract-class)
- [III. Tính trừu tượng:](#iii-tính-trừu-tượng)
- [IV. Sự khác nhau của Abstract Class và Interface:](#iv-sự-khác-nhau-của-abstract-class-và-interface)


# I. Interface là gì?
- **Interface**: là 1 một bản thiết kế giữa các lớp chỉ định các phương thức và các trường (biến, thuộc tính) cần có trong các lớp được triển khai
- Có 2 thành phần chính: 
  - **Các trường** : Giá trị các trường không thể thay đổi và có thể truy cập từ bất kì đối tượng nào. Được mặc định là:
    -  **public** : các trường khai báo trong interface được truy cập công khai từ bên ngoài
    -  **static** : có thể được truy cập mà không cần khởi tạo 1 thể hiện nào của interface 
    -  **final** : giá trị các trường không thể thay đổi
    ```java
    interface DongVat {
        String maulong1 = "Vàng";
        public static final String maulong2 = "Đen";
        void hanhDong();
    }


    public class Main {
        public static void main(String[] args) {
            System.out.println(DongVat.maulong1);
            System.out.println(DongVat.maulong2);
        }
    }
    ```

  - **Các phương thức trừu tượng** : các phương thức chỉ được khai báo nhưng không có cách triển khai hoặc thân hàm. 
    - Khi lớp nào triển khai interface, trừ lớp trừu tượng abstract, lớp đó phải bắt buộc triển khai các phương thước trừu tượng trong interface 
    - Theo mặc định: các phương thức trong interface đều là **public** và **abstract**
    
    ```java
    interface DongVat {
        String maulong1 = "Vàng";
        public static final String maulong2 = "Đen";
        void hanhDong();
    }

    class Meo implements DongVat {
        @Override
        public void hanhDong() {
            System.out.println("Kêu Meo Meo");
        }
    }

    class Cho implements DongVat {
        @Override
        public void hanhDong() {
            System.out.println("Kêu Gâu Gâu");
        }
    }
    public class Main {
        public static void main(String[] args) {
            ArrayList<DongVat> dongVats = new ArrayList<>();
            dongVats.add(new Meo());
            dongVats.add(new Cho());
            for(DongVat dongVat : dongVats){
                dongVat.hanhDong();
            }
        }
    }
    ```
        Kết quả:
        Kêu Meo Meo
        Kêu Gâu Gâu
- Từ Java 8, xuất hiện phương thức mặc định (Default Method): là phương thức được triển khai sẵn -> Giúp tăng cường tính linh hoạt của interface và giúp dễ mở rộng hơn không làm ảnh hưởng đến các lớp đã triển khai
```java
interface DongVat {
        String maulong1 = "Vàng";
        public static final String maulong2 = "Đen";

        void hanhDong();

        default void An() {
            System.out.println("Dộng vật đang ăn");
        }
    }
```

- Đa kế thừa trong Java bởi interface:

```java
interface DongVat {
    void an();
}

interface GiaCam {
    void co2chan();
}

class Ga implements DongVat, GiaCam {
    @Override
    public void an() {
        System.out.println("Động vật đang ăn");
    }
    @Override
    public void co2chan() {
        System.out.println("Động vật có 2 chân");
    }

    public static void main(String[] args) {
        Ga ga = new Ga();
        ga.an();
        ga.co2chan();
    }
}
```

# II. Abstract Class
- **Abstract Class (lớp trừu tượng)** : là 1 loại lớp đặc biệt trong Java không thể tự khởi tạo được (không thể tạo đối tượng từ lớp trừu tượng), nó được sử dụng như 1 bản thiết kế để tạo ra các lớp con
- Để sử dụng abstract class cần có 1 lớp không phải lớp trừu tượng và lớp này sẽ nới rộng và trở thành lớp con của lớp trừu tượng

```java
abstract class DongVat {
    public void ngu() {
        System.out.println("Động vật đang ngủ");
    }
}

class Meo extends DongVat {
    
}

class Main {
    public static void main(String[] args) {
        DongVat dongVat = new Meo();
        dongVat.ngu();
    }
}
```
    Kết quả : Động vật đang ngủ

- **Phương thức trừu tượng** : là 1 phương thức được khai báo là abstract và không có trình triển khai

    Nếu bạn muốn một lớp chứa một phương thức cụ thể nhưng bạn muốn triển khai thực sự phương thức đó để được quyết định bởi các lớp con, thì bạn có thể khai báo phương thức đó trong lớp cha ở dạng abstract.

- Trong Java, lớp nào kế thừa lớp trừu tượng sẽ phải triển khai tất cả các phương thức trừu tượng của lớp cha

```java
abstract class DongVat {
    abstract void keu();
}

class Meo extends DongVat {
    @Override
    void keu() {
        System.out.println("Meo meo");
    }
}
class Main {
    public static void main(String[] args) {
        DongVat dongVat = new Meo();
        dongVat.keu();
    }
}
```

# III. Tính trừu tượng: 
- **Tính trừu tượng** là một tiến trình ẩn các cài đặt chi tiết và chỉ hiển thị tính năng tới người dùng.

    Nói cách khác, nó chỉ hiển thị các thứ quan trọng tới người dùng và ẩn các chi tiết nội tại, ví dụ: để gửi tin nhắn, người dùng chỉ cần soạn text và gửi tin. Bạn không biết tiến trình xử lý nội tại về phân phối tin nhắn.

- Tính trừu tượng giúp bạn trọng tâm hơn vào đối tượng thay vì quan tâm đến cách nó thực hiện.

- Có 2 cách để đạt được sự trừu tượng hóa trong Java:
  - Sử dụng lớp abstract
  - Sử dụng interface

# IV. Sự khác nhau của Abstract Class và Interface:

| Abstract Class | Interface |
|-------|-------|
| Có phương thức abstract (không có thân hàm) và phương thức non-abstract (có thân hàm). | Chỉ có phương thức abstract. Từ java 8, nó có thêm các phương thức default và static. | 
| Abstract class **không hỗ trợ đa kế thừa** | Interface **có hỗ trợ đa kế thừa** |
| Có các biến final, non-final, static and non-static. | Chỉ có các biến static và final. |
|  Abstract class có thể cung cấp nội dung cài đặt cho phương thức của interface. | Interface không thể cung cấp nội dung cài đặt cho phương thức của abstract class. |
| Các phương thức trong abstract class có thể là public hoặc protected | Các phương thức trong interface luôn luôn phải để là public |
| Khi một nhóm đối tượng có cùng bản chất kế thừa từ một class thì sử dụng abstract class. | Khi một nhóm đối tượng không có cùng bản chất nhưng chúng có hành động giống nhau thì sử dụng interface. |
