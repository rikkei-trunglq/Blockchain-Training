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
- Để khai báo một hằng số(constant) thêm từ khóa `constant` sau kiểu dữ liệu
```
    uint constant x = 32**22 + 8;
    string constant text = "abc";
    bytes32 constant myHash = keccak256("abc");
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

### `Contructor` trong Contract 
- `contructor` là một function có thể có hoặc không khi viết một Contract
- `contructor` được chạy khi Contract được khởi tạo
- Một function `contructor` có thể là `public` hoặc `internal`. Nếu không có function `contructor` khi khởi tạo Contract một `default contructor` sẽ được thực thi

```
pragma solidity >=0.5.0 <0.7.0;

contract A {
    uint public a;

    constructor(uint _a) internal {
        a = _a;
    }
}

contract B is A(1) {
    // default contructor
    constructor() public {}
}
```

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
- `Functions` hỗ trợ trả về nhiều giá trị
- Một số phạm vi truy cập của `Function`:
   - `public` là các `function` có thể được gọi trong Contract và ngoài Contract

     ```
     contract FirstContract {
        uint public publicVariable;
    
        constructor() public {
           publicVariable = 10;
        }

        // public function
        function incrVariable(uint number) public {
          publicVariable = publicVariable + number;
        }

        function executeIncrement(uint number) public {
          // được gọi trong Contract
          incrVariable(number);
        }
     }

     contract SecondContract {
        FirstContract firstContract = new FirstContract();
    
        function executeIncrement(uint number) public {
            // được gọi tại một Contract khác
            firstContract.incrVariable(number);
        }
     }

     contract ThirdContract is FirstContract {
        function executeIncrementThrid(uint number) public {
            // được gọi tại Contract kế thừa sử dụng this
            this.incrVariable(number);
        }
     }
     ```
   - `external` là các `function` chỉ thể được gọi ngoài Contract chứa nó

     ```
     contract FirstContract {
        uint public publicVariable;
    
        constructor() public {
           publicVariable = 10;
        }

        // external function
        function incrVariable(uint number) external {
          publicVariable = publicVariable + number;
        }

        function executeIncrement(uint number) public {
          // báo lỗi vì nó không thể gọi bên trong Contract chứa nó
          incrVariable(number);
        }
     }

     contract SecondContract {
        FirstContract firstContract = new FirstContract();
    
        function executeIncrement(uint number) public {
            // được gọi tại một Contract khác
            firstContract.incrVariable(number);
        }
     }

     contract ThirdContract is FirstContract {
        function executeIncrementThrid(uint number) public {
            // được gọi tại Contract kế thừa sử dụng this
            this.incrVariable(number);
        }
     }
     ```
   - `private` là các `function` chỉ thể được gọi trong Contract chứa nó và các Contract kế thừa

     ```
     contract FirstContract {
        uint public publicVariable;
    
        constructor() public {
           publicVariable = 10;
        }

        // private function
        function incrVariable(uint number) private {
          publicVariable = publicVariable + number;
        }

        function executeIncrement(uint number) public {
          // gọi bên trong Contract
          incrVariable(number);
        }
     }

     contract SecondContract {
        FirstContract firstContract = new FirstContract();
    
        function executeIncrement(uint number) public {
            // Báo lỗi vì không thể gọi bên ngoài Contract
            firstContract.incrVariable(number);
        }
     }

     contract ThirdContract is FirstContract {
        function executeIncrementThrid(uint number) public {
            // Báo lỗi vì không thể gọi bên ngoài Contract
            this.incrVariable(number);
        }
     }
     ```
   - `internal` là các `function` chỉ thể được gọi trong Contract chứa nó và các Contract kế thừa

     ```
     contract FirstContract {
        uint public publicVariable;
    
        constructor() public {
           publicVariable = 10;
        }

        // internal function
        function incrVariable(uint number) internal {
          publicVariable = publicVariable + number;
        }

        function executeIncrement(uint number) public {
          // gọi bên trong Contract
          incrVariable(number);
        }
     }

     contract SecondContract {
        FirstContract firstContract = new FirstContract();
    
        function executeIncrement(uint number) public {
            // Báo lỗi vì không thể gọi bên ngoài Contract
            firstContract.incrVariable(number);
        }
     }

     contract ThirdContract is FirstContract {
        function executeIncrementThrid(uint number) public {
            // gọi bên trong Contract kế thừa
            incrVariable(number);
        }
     }
     ```
- Một số loại `Function`:
   - `View Function` là các `function` đảm bảo không làm thay đổi trạng trái, một số trường hợp sau được tính là sẽ làm thay đổi trạng thái:

      - Thay đổi giá trị của State Variables

      - Emit Events

      - Khởi tạo Contract mới

      - Sử dụng `selfdestruct`(Tìm hiểu sau)

      - Sending Ether via calls.(Tìm hiểu sau)

      - Gọi một `function` khác không phải là `view` hoặc `pure`

      - Using low-level calls(Tìm hiểu sau)

      - Using inline assembly that contains certain opcodes.(Tìm hiểu sau)

   - Các function `Getter` luôn là các `View Function`

   ```
    contract FirstContract {
        uint public publicVariable;
        int private privateVariable;
        string internal internalVariable;
        
        constructor() public {
            publicVariable = 10;
            privateVariable = -20;
            internalVariable = 'Ahihi';
        }
        
        function getPrivateVariable() public view returns (int) {
            return privateVariable;
        }
        
        function getInternalVariable() public view returns (string memory) {
            return internalVariable;
        }
    }
   ```
   - `Pure Function` là các `function` đảm bảo không đọc hoặc làm thay đổi trạng trái, ngoài một số trường hợp làm thay đổi trạng thái như ở phần View thì một số trường hợp sau được tính là đọc từ trạng thái:

      - Lấy giá trị từ State Variables

      - Sử dụng `address(this).balance` hoặc `<address>.balance`

      - Accessing any of the members of block, tx, msg (with the exception of msg.sig and msg.data)(Tìm hiểu sau)

      - Gọi một `funtion` khác không phải `pure`

      - Using inline assembly that contains certain opcodes.(Tìm hiểu sau)

   ```
    contract FirstContract {
        function calculate() public pure returns (int) {
            return 5 * 5;
        }
    }
   ```
   - `Fallback Function` là các `function` được thực thi bất cứ khi nào mà nó nhận được Ether, nhận Ether và thêm nó vào tổng số dư của Contract. `Fallback Function` phải được gán mác `payable`, nếu không Contract sẽ không thể nhận Ether và trả ra exception.
   ```
    contract OnlineStore {
      function buySomething() external payable {
        // Check to make sure 0.001 ether was sent to the function call:
        require(msg.value == 0.001 ether);
        // If so, some logic to transfer the digital item to the caller of the function:
        transferThing(msg.sender);
      }
    }
   ```
   - `Function Overloading` trong một Contract có thể có nhiều function cùng tên nhưng khác loại tham số đầu vào. `overloading` thường được áp dụng trong kế thừa
   ```
    pragma solidity >=0.4.16 <0.7.0;

    contract A {
        function f(uint _in) public pure returns (uint out) {
            out = _in;
        }

        function f(uint _in, bool _really) public pure returns (uint out) {
            if (_really)
                out = _in;
        }
    }
   ```

### `Events` trong Contract 
- `Event` là cách để Contract thông báo có điều gì xảy ra với Blockchain trên giao diện người dùng của ứng dụng. Có thể lắng nghe và đưa ra hành động xử lý khi có vấn đề.

  ```
  // declare the event
  event IntegersAdded(uint x, uint y, uint result);

  function add(uint _x, uint _y) public returns (uint) {
    uint result = _x + _y;
    // fire an event to let the app know the function was called:
    emit IntegersAdded(_x, _y, result);
    return result;
  }
  ```
  In front-end
  ```
  YourContract.IntegersAdded(function(error, result) {
    // do something with result
  })
  ```
### `Function Modifiers` trong Contract 
- `Function Modifier` sử dụng để thay đổi hành vi của một function, được sử dụng để thêm các tiền xử lý vào trong function, các tiền xử lý sẽ được thực thi trước khi chạy các logic ban đầu của function

  ```
  pragma solidity ^0.5.0;

  contract Owner {
    address owner;
    constructor() public {
        owner = msg.sender;
    }

    // Function Modifier kiểm tra xem người gửi có phải là 'owner' hay không
    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }

    // Function Modifier kiểm tra xem giá được nhập có lớn hơn giá ban đầu không
    modifier costs(uint price) {
        if (msg.value >= price) {
          _;
        }
    }
  }
  contract Register is Owner {
    mapping (address => bool) registeredAddresses;
    uint price;
    constructor(uint initialPrice) public { price = initialPrice; }
    
    // Thêm Function Modifier vào trong function
    function register() public payable costs(price) {
        registeredAddresses[msg.sender] = true;
    }

    // Thêm Function Modifier vào trong function
    function changePrice(uint _price) public onlyOwner {
        price = _price;
    }
  }
  ```
