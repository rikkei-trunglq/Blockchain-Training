# Solidity Basic

## Data types(Kiểu dữ liệu)
- bool: Kiểu dữ liệu logic
- int/uint: Kiểu dữ liệu số nguyên, bao gồm 256 bit
- int8 to int256: Kiểu dữ liệu số nguyên từ 8 bit đến 256 bit, một số kiểu ví dụ như:

  int8(8 bit) có range từ -128 đến 127

  int16(16 bit) có range từ -32,768 đến 32,767

  int32(32 bit) có range từ -2,147,483,648 đến 2,147,483,647

  int64(64 bit) có range từ -9,223,372,036,854,775,808 đến 9,223,372,036,854,775,807

  ...
- uint8 đến uint256: Kiểu dữ liệu số nguyên dương từ 8 bit đến 256 bit, một số kiểu ví dụ như:

  uint8(8 bit) có range từ 0 đến 255

  uint16(16 bit) có range từ 0 đến 65,535

  uint32(32 bit) có range từ 0 đến 4,294,967,295

  uint64(64 bit) có range từ 0 đến 18,446,744,073,709,551,615

  ...

- fixed/unfixed: Kiểu dữ liệu số thập phân (Không còn được hỗ trợ trong Solidity)
- string: Kiểu dữ liệu chuỗi, có thể được đặt trong dấu "" hoặc ''
- struct: Kiểu dữ liệu cấu trúc, bao gồm nhiều thành phần bên trong
- address: Mỗi Ethereum blockchain ví như một account, address là một chuỗi định dạng duy nhất trỏ đến địa chỉ của account đó
- enum: Liệt kê một hoặc nhiều giá trị được chỉ định trước
```
    // Kiểu dữ liệu logic
    bool isCheck = true;
    
    // Kiểu dữ liệu số nguyên
    int firstNumber = -10;

    // Kiểu dữ liệu số nguyên dương
    uint secondNumber = 100;

    // Kiểu dữ liệu chuỗi
    string name = "Le Quang Trung";
    // Chuỗi được diễn giải ở dạng byte nếu kiểu dữ liệu được để là byte
    byte32 temp = "stringliteral";

    // Kiểu struct
    struct Zombie {
        string name;
        uint dna;
    }

    // Kiểu địa chỉ
    address ckAddress = 0x06012c8cf97BEaD5deAe237070F9587f8E7A266d;

    // Kiểu enum
    enum FreshJuiceSize{ SMALL, MEDIUM, LARGE }
    FreshJuiceSize choice = FreshJuiceSize.LARGE;
```

## Variables(Biến)
- State Variables: Biến khai báo và lưu trữ trong Contract
- Local Variables: Biến được khai báo trong function và có giá trị trong khi function được thực thi
- Global Variables: Một số biến đặc biệt có phạm vi Global được sử dụng, một ví dụ hay sử dụng nhất là `msg.sender` hình dung đơn giản là bạn có một function và nhiều người cùng gọi function đấy của bạn thì `msg.sender` là địa chỉ của từng người gọi function đó.
```
contract ZombieFactory {
    uint dnaDigits = 16; -- State Variables
    
    function _generateRandomDna(string memory _str) private view returns (uint) {
        uint rand = uint(keccak256(abi.encodePacked(_str)));  -- Local Variables
        return rand % dnaModulus;
    }
}
```

## Operator(Toán tử)
- Toán tử toán học

    -- Subtraction(-)
        ```
        uint dnaDigits = 16 - 10;
        ```
        
    -- Addition(+)
        ```
        uint dnaDigits = 16 + 10;
        ```
        
    -- Multiplication(*)
        ```
        uint dnaDigits = 16 * 10;
        ```
        
    -- Division(/)
        ```
        uint dnaDigits = 10 / 2;
        ```
        
    -- Modulus(%)
        ```
        uint dnaDigits = 10 / 3;
        ```
        
    -- Increment(++)
        ```
        uint dnaDigits = 10;
        dnaDigits++;
        ```
        
    -- Decrement(--)
        ```
        uint dnaDigits = 10;
        dnaDigits--;
        ```
- Toán tử so sánh

  -- Equal(`==`)

  -- Not Equal(`!=`)

  -- Greater than(`>`)

  -- Less than(`<`)

  -- Greater than or Equal to(`>=`)

  -- Less than or Equal to(`<=`)

- Toán tử logic

  -- Logical AND(`&&`)

  -- Logical OR(`||`)

  -- Logical NOT(`!`)

## Loops(Vòng lặp)
- While Loop
    ```
        uint count;
        while (count < 10) {
            count++;
        }
    ```
- Do - While loop
    ```
        uint count;
        do{
            count--;
         }while(count > 0) ;
            count++;
        }
    ```
- For loop
    ```
        uint count;
        for(uint i=0; i<5; i++){
            count++;
        }
    ```
    
## Arrays(Mảng)
- Cú pháp khởi tạo mảng
  `<data type> <array name>[size] = <initialization>`

- Mảng tĩnh: Mảng với kích thước phần tử được cấu hình trước, số phần tử trong mảng không được vượt quá kích thước mảng.
    ```
    // Khai báo một mảng numbers có kích thước là 10 và numberss có kích thước là 4
    uint numbers[10];
    uint numberss[4] = [1,2,3,4]
    ```
- Mảng động: Mảng với kích thước phần tử không được cấu hình trước, mỗi khi thêm phần tử vào trong mảng thì kích thước của mảng sẽ được thay đổi
    ```
    uint numbers[];
    uint[] balance = new uint[](5);
    ```
- Tương tác với mảng
    ```
    uint[] numbers = new uint[](5);
    // Thêm phần tử vào mảng
    numbers.push(5);
    numbers.push(10);
    numbers.push(15);

    // Lấy ra giá trị của phần tử theo vị trí numbers[index]
    uint temp = numbers[1];

    // Lấy ra độ dài của mảng
    uint size = numbers.length;

    // Xóa phần từ cuối cùng trong mảng
    numbers.pop();
    ```

## Mappings
Mapping là các cặp key-value để lưu trữ và truy xuất dữ liệu, Mapping cũng giống như Map ở Java
```
// Tạo một mapping có key là kiểu uint và value là kiểu string
mapping (uint => string) idToName;

// Push cặp key-value vào trong mapping
idToName[1] = "Trung123";

// Lấy ra value từ key trong mapping
string name = idToName[1];
```

## Contract
- Contract trong Solidity cũng giống như Class trong Java hay C#, nó biểu thị một đối tượng. 
- Mỗi Contract có thể chứa các `State Variables`, `Functions`, `Function Modifier`, `Events`, `Structs`, `Enums`.
- Contract hỗ trợ tính kế thừa.

### `State variables` trong Contract 
- Các `State Variables` là các biến được lưu trữ trong Contract.
- Một số phạm vi truy cập của `State Variables`:

   - `public` là các biến có thể gọi và sử dụng trong nội bộ Contract và các Contract kế thừa, đặc điểm của các biến public là không cần viết hàm `get` vì các biến public được tự động tạo hàm `get`.

     ```
     contract FirstContract {
        uint public publicVariable;
    
        constructor() public {
           publicVariable = 10;
        }
     }

     contract SecondContract {
        FirstContract firstContract = new FirstContract();
    
        function getPublicVar() public view returns(uint) {
            return firstContract.publicVariable(); -- Gọi trức tiếp thông qua hàm get tự gen
        }
     }

     contract ThirdContract is FirstContract {
        function getPublicVarThird() public view returns(uint) {
            return publicVariable;  -- Gọi trực tiếp
        }
     }
     ```
   - `internal` là các biến được sử dụng trong nội bộ Contract và các Contract kế thừa mà không cần hàm `get`, đối với các Contract khác muốn sử dụng các biến `internal` bắt buộc phải gọi thông qua hàm `get`

     ```
     contract FirstContract {
        string internal internalVariable;
    
        constructor() public {
           internalVariable = 'Ahihi';
        }

        function getInternalVariable() public view returns (string memory) {
           return internalVariable;
        }
     }

     contract SecondContract {
        FirstContract firstContract = new FirstContract();
    
        function getInternalVar() public view returns(string memory) {
           return firstContract.getInternalVariable(); -- Gọi thông qua hàm get
        }
     }

     contract ThirdContract is FirstContract {
        function getInternalVarThird() public view returns(string memory) {
            return internalVariable;  -- Gọi trực tiếp do kế thừa
        }
     }
     ```
   - `private` là các biến chỉ sử dụng được trong nội bộ Contract, các Contract kế thừa hoặc Contract khác không thể sử dụng các biến này trừ khi thông qua hàm `get`

     ```
     contract FirstContract {
        int private privateVariable;
    
        constructor() public {
           privateVariable = -20;
        }

        function getPrivateVariable() public view returns (int) {
           return privateVariable;
        }
     }

     contract SecondContract {
        FirstContract firstContract = new FirstContract();
    
        function getPrivateVar() public view returns(int) {
           return firstContract.getPrivateVariable(); -- Gọi thông qua hàm get
        }
     }

     contract ThirdContract is FirstContract {
        function getPrivateVarThird() public view returns(int) {
            return getPrivateVariable();  -- Gọi thông qua hàm get
        }
     }
     ```
### `Functions` trong Contract 
- `Functions` là bộ hành vi trong Contract
- Một số phạm vi truy cập của `Function`:
