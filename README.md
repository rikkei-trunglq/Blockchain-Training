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
        uint dnaDigits = 10 % 3;
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
   - `private` là các `function` chỉ thể được gọi trong Contract chứa nó

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
## Data Locations - `Storage`, `Memory` and `Calldata`
- Khi khai báo các biến, chúng có thể được chỉ định rõ nơi lưu trữ thông qua 3 nơi lưu trữ sau:

  - `storage` tại vị trí nơi mà các biến `State Variable` được lưu trữ trên Blockchain

    ```
    pragma solidity >=0.4.0 <0.7.0;

    contract C {
        uint[] x; // the data location of x is storage

        function f(uint[] memory memoryArray) public {
            x = memoryArray; // works, copies the whole array to storage
            uint[] storage y = x; // works, assigns a pointer, data location of y is storage
        }
    }
    ```

  - `memory` là các biến lưu trữ local, lưu trữ theo function, khi function thực hiện xong biến sẽ được giải phóng. Với các kiểu dữ liệu như `arrays`, `structs`, `mappings` và `strings` cần phải lưu trữ `memory`
  
    ```
    pragma solidity >=0.5.0 <0.6.0;

    contract ZombieFactory {

        function createZombie (string memory _name, uint _dna) public {
            // ...
        }

    }
    ```

  - `calldata` là các biến read-only, không thể thay đổi được lưu trữ lại nơi lưu trữ các tham số của function, chỉ tồn lại trong quá trình thực thi function. Chỉ khả dụng với `external` function.
    
    ```
    contract FirstContract {

        // Báo lỗi do không thể thay đổi được giá trị của biến được
        function demoCallData(string calldata name) external {
            name = "trung ne";
        }

        // sử dụng calldata với external function
        function demoCallDataV2(string calldata name) external {
            // todo
        }
    }
    ```
## `Inheritance`(Tính kế thừa giữa các Contract)
- Khi một Contract kế thừa từ một Contract khác, chỉ duy nhất một Contract được khởi tạo trong Blockchain, toàn bộ code của Contract mà nó kế thừa sẽ đều được compile vào trong Contract đã được tạo

  ```
  pragma solidity >=0.5.0 <0.6.0;

  contract FirstContract {
      uint public publicVariable;
      int private privateVariable;
      string internal internalVariable;
      
      constructor() public {
          publicVariable = 10;
          privateVariable = -20;
          internalVariable = 'Ahihi';
      }
      
      function incrVariable(uint number) internal {
          publicVariable = publicVariable + number;
      }
  }

  contract ThirdContract is FirstContract {
      
      // Sử dụng super để gọi các đến internal function của Contract cha
      function executeIncrementThrid(uint number) public {
          super.incrVariable(number);
      }
  }
  ```
- Solidity hỗ trợ đa kế thừa

  ```
  pragma solidity >=0.5.0 <0.6.0;

  contract FirstContract {}
  contract SecondContract {}
  contract ThirdContract is FirstContract, SecondContract{}
  ```
  - `Diamond Problem` trong đa kế thừa
  
  Ví dụ:
  
  Có một Contract là `Everything` chứa một function là `breathe()`
  ```
  pragma solidity >=0.5.0 <0.6.0;

  import "hardhat/console.sol";

  contract Everything {

    constructor() public {
        console.log("Everything");
    }

    function breathe() public {
      console.log("Everything breathe!");
    }
  }
  ```
  Một Contract thứ hai là `Animal` kế thừa từ Contract `Everything` và override lại phương thức `breathe()`
  ```
  pragma solidity >=0.5.0 <0.6.0;

  import "hardhat/console.sol";

  contract Everything {

    constructor() public {
        console.log("Everything");
    }

    function breathe() public {
      console.log("Everything breathe!");
    }
  }

  contract Animal is Everything {

    constructor() public {
        console.log("Animal");
    }

    function breathe() public {
      console.log("Animal breathe!");
    }
  }
  ```
  Một Contract thứ ba là `People` kế thừa từ Contract `Everything` và override lại phương thức `breathe()`
  ```
  pragma solidity >=0.5.0 <0.6.0;

  import "hardhat/console.sol";

  contract Everything {

    constructor() public {
        console.log("Everything");
    }

    function breathe() public {
      console.log("Everything breathe!");
    }
  }

  contract Animal is Everything {

    constructor() public {
        console.log("Animal");
    }

    function breathe() public {
      console.log("Animal breathe!");
    }
  }

  contract People is Everything {

    constructor() public {
        console.log("People");
    }

    function breathe() public {
      console.log("People breathe!");
    }
  }
  ```
  Một Contract thứ tư là `XMen` kế thừa từ Contract `Animal`, `People` và override lại phương thức `breathe()`
  ```
  pragma solidity >=0.5.0 <0.6.0;

  import "hardhat/console.sol";

  contract Everything {

    constructor() public {
        console.log("Everything");
    }

    function breathe() public {
      console.log("Everything breathe!");
    }
  }

  contract Animal is Everything {

    constructor() public {
        console.log("Animal");
    }

    function breathe() public {
      console.log("Animal breathe!");
    }
  }

  contract People is Everything {

    constructor() public {
        console.log("People");
    }

    function breathe() public {
      console.log("People breathe!");
    }
  }

  contract XMen is Animal,People {
    
    constructor() public {
        console.log("XMen");
    }
    
    function breathe() public view {
        console.log("XMen breathe!");
    }
  }
  ```
  Trong trường hợp này Contract muốn override lại phương thức `breathe()` nhưng kế thừa từ 2 Contract là `Animal` và `People` nên sẽ không biết phải override phương thức `breathe()` từ Contract nào => Vấn đề này được gọi là `Diamond Problem`

  Solidity đã giải quyết vấn đề này bằng cách áp dụng giải thuật `C3 linearization` như sau:

  ```
  // Contract `Everything`
  // Contract `Animal` kế thừa Contract `Everything`
  // Contract `People` kế thừa Contract `Everything`
  // Contract `XMen` kế thừa Contract `Animal` và `People`

  L(Everything) = [Everything]

  L(Animal)     = [Animal] + Merge(L(Everything), [Everything])
                = [Animal] + Merge([Everything], [Everything])
                = [Animal, Everything]

  L(People)     = [People] + Merge(L(Everything), [Everything])
                = [People] + Merge([Everything], [Everything])
                = [People, Everything]

  L(XMen)       = [XMen] + Merge(L(Animal), L(People), [Animal, People])
                = [XMen] + Merge([Animal, Everything], [People, Everything], [Animal, People])
                = [XMen, Animal] + Merge([Everything], [People, Everything], [People])
                = [XMen, Animal, People] + Merge([Everything], [Everything])
                = [XMen, Animal, People, Everything]
  ```
  => Nhận thấy thứ tự Contract được gọi sẽ như sau: `Everything => People => Animal => XMen`
  
  ✨Thực tế thứ tự Contract được gọi khi deploy đoạn code trên là `Everything => Animal => People => XMen`. Nguyên nhân là thứ tự Contract kế thừa sẽ bị đảo ngược lại thành✨

  ```
  L(XMen)       = [XMen] + Merge(L(People), L(Animal), [People, Animal])
                = [XMen] + Merge([People, Everything], [Animal, Everything], [People, Animal])
                = [XMen, People] + Merge([Everything], [Animal, Everything], [Animal])
                = [XMen, People, Animal] + Merge([Everything], [Everything])
                = [XMen, People, Animal, Everything]
  ```
  => Thứ tự Contract được đúng sẽ là `Everything => Animal => People => XMen`
  
# ERC20

Trong Ethereum, ERC là một Yêu cầu nhận xét của Ethereum (Ethereum Request for Comments). Đây là những tài liệu kỹ thuật phác thảo các tiêu chuẩn để lập trình trên Ethereum. Không nên nhầm lẫn chúng với Đề xuất cải tiến Ethereum (tức các EIP). Giống như BIP của Bitcoin, EIP là những đề xuất cải tiến cho chính giao thức. Thay vào đó, các ERC nhằm mục đích thiết lập các quy ước giúp các ứng dụng và hợp đồng tương tác với nhau dễ dàng hơn.

Được đề xuất bởi Vitalik Buterin và Fabian Vogelsteller vào năm 2015, ERC-20 đề xuất một định dạng tương đối đơn giản cho các token hoạt động trên Ethereum. Bằng cách làm theo phác thảo, các nhà phát triển không cần phải phát minh lại cấu trúc nào khác. Thay vào đó, họ có thể xây dựng trên một nền tảng đã được sử dụng trong toàn ngành.

Không giống như ETH (tiền mã hoá gốc của Ethereum), các token ERC-20 không được giữ bởi tài khoản. Các token này chỉ tồn tại trong một hợp đồng, giống như một cơ sở dữ liệu độc lập. Nó chỉ định các quy tắc cho các token (như tên, ký hiệu, khả năng phân chia) và giữ một danh sách ánh xạ số dư của người dùng đến địa chỉ Ethereum của họ.

Để tuân thủ ERC-20, hợp đồng của bạn cần bao gồm sáu chức năng bắt buộc: `totalSupply` , `balanceOf` , `transfer` , `transferFrom` , `approve` và `allowance` . Ngoài ra, bạn có thể chỉ định các chức năng tùy chọn, chẳng hạn như `name`, `symbol` và `decimal`.

## totalSupply
```
function totalSupply() public view returns (uint256)
```

Khi được người dùng gọi, hàm trên trả về tổng nguồn cung token mà hợp đồng nắm giữ.

## balanceOf
```
function balanceOf (address _owner) public view trả về (uint256 balance)
```

Không giống như `totalSupply`, `balanceOf` nhận một tham số (một địa chỉ). Khi hàm được gọi, nó trả về số dư token mà địa chỉ đó đang nắm giữ. Hãy nhớ rằng các tài khoản trên mạng Ethereum là công khai, vì vậy bạn có thể truy vấn số dư của bất kỳ người dùng nào mà bạn biết địa chỉ.

## transfer
```
function transfer(address _to, uint256 _value) public returns (bool success)
```

Tính năng `transfer` chuyển một cách khéo léo các token từ người dùng này sang người dùng khác. Tại đây, bạn cung cấp địa chỉ muốn gửi và số tiền cần chuyển.
Khi tính năng được gọi, transfer sẽ kích hoạt một thứ được gọi là event (trong trường hợp này là event transfer). Về cơ bản, điều này yêu cầu blockchain bao gồm một tham chiếu đến nó.

## transferFrom
```
function transferFrom(address _from, address _to, uint256 _value) public returns (bool success)
```

Chức năng `transferFrom` là một sự thay thế tiện dụng hơn so với chức năng transfer. Nó cho phép lập trình nhiều hơn một chút trong các ứng dụng phi tập trung. Giống như transfer, nó được sử dụng để di chuyển token, nhưng những token đó không nhất thiết phải thuộc về người gọi hợp đồng. 
Nói cách khác, bạn có thể ủy quyền cho ai đó– hoặc một hợp đồng khác – thay mặt bạn chuyển tiền. Lấy ví dụ như khi bạn cần thanh toán cho các dịch vụ trả phí theo thời gian, khi bạn không muốn tốn thời gian gửi thanh toán theo cách thủ công hàng ngày/tuần/tháng. Thay vào đó, bạn chỉ cần để một chương trình làm việc đó tự động cho bạn.

Hàm này kích hoạt cùng một sự kiện như `transfer`.

## approve
```
function approve(address _spender, uint256 _value) public returns (bool success)
```

`approve` là một chức năng hữu ích và có nhiều hướng để lập trình. Với chức năng này, bạn có thể giới hạn số lượng token mà một hợp đồng thông minh có thể rút từ số dư của bạn. Nếu không có nó, bạn phải đối mặt với nguy cơ hợp đồng bị trục trặc (hoặc bị lợi dụng) và tất cả tiền của bạn có khả năng bị đánh cắp. 

Lấy ví dụ về một mô hình đăng ký (subscription) một lần nữa. Giả sử rằng bạn có một lượng lớn BinanceAcademyTokens và bạn muốn thiết lập các khoản thanh toán định kỳ hàng tuần cho một DApp trực tuyến. Vì bận rộn đọc các bài viết của Binance Academy cả ngày lẫn đêm, bạn không muốn mất thời gian tạo giao dịch theo cách thủ công mỗi tuần.

Và bạn cũng có một số dư lớn BinanceAcademyTokens, vượt xa số tiền cần thanh toán. Để ngăn DApp rút hết tiền, bạn có thể đặt giới hạn bằng chức năng approve. Giả sử, việc đăng ký dịch vụ khiến bạn tốn một BinanceAcademyToken mỗi tuần. Nếu bạn giới hạn giá trị được phê duyệt ở mức 20 token, bạn có thể chọn thanh toán tự động cho đăng ký của mình trong năm tháng.

Tệ nhất, nếu DApp cố gắng rút tất cả tiền của bạn hoặc nếu phát hiện thấy lỗi, bạn chỉ có thể mất hai mươi token. Điều kiện này không phải là lý tưởng, nhưng ít nhất nó không khiến bạn mất tất cả tài sản mình đang nắm giữ.

Khi được gọi, approve sẽ kích hoạt sự kiện approval. Giống như sự kiện trong transfer, chức năng approve cũng ghi dữ liệu vào blockchain.

## allowance 
```
function allowance(address _owner, address _spender) public view returns (uint256 remaining)
```

`allowance` có thể được sử dụng cùng với approve . Khi bạn đã cho phép hợp đồng quản lý các token của mình, bạn có thể sử dụng quyền này để kiểm tra xem nó vẫn có thể rút được bao nhiêu tiền. Ví dụ: nếu gói đăng ký của bạn đã sử dụng hết mười hai trong số hai mươi token được chấp thuận của bạn, thì việc gọi hàm allowance sẽ trả về tổng số là tám.


# ERC1155

ERC-1155 là một tiêu chuẩn token kỹ thuật số do Enjin tạo ra có thể được sử dụng để tạo cả tài sản có Fungible (tiền tệ) và Non-Fungible (thẻ kỹ thuật số, vật nuôi và các vật phẩm trong game) trên mạng lưới Ethereum. Bằng cách sử dụng mạng Ethereum, ERC-1155 token an toàn, có thể giao dịch và miễn nhiễm với hack.

ERC-1155 một cách mới để tạo token cho phép thực hiện các giao dịch và gói giao dịch hiệu quả hơn – do đó tiết kiệm chi phí. Tiêu chuẩn token này cho phép tạo ra cả token tiện ích (chẳng hạn như BNB hoặc BAT) và cả các Non-Fungible Token như CryptoKitties.

ERC-1155 bao gồm các tối ưu hóa cho phép thực hiện các giao dịch hiệu quả hơn và an toàn hơn. Các giao dịch có thể được nhóm lại với nhau – do đó giảm chi phí chuyển token. ERC-1155 được xây dựng dựa trên công việc trước đó như ERC-20 (token tiện ích) và ERC-721 (các vật phẩm sưu tầm hiếm).

## Sự Khác Nhau Giữa ERC-1155 và ERC-721

Tiêu chuẩn(standard) là tập hợp các quy tắc xác định dữ liệu thể hiện các chức năng mà mỗi token có thể thực hiện.

Tất cả những NFT khi được tạo ra là không giống nhau, điều này rõ ràng hơn khi đem so sánh hai tiêu chuẩn ERC-1155 và ERC-721. 

Tiêu chuẩn ERC-1155 được tạo ra với các chức năng tương tự như một chiếc máy bán hàng tự động, nơi mà các nhà phát triển có thể triển khai một hợp đồng thông minh, cái mà có thể được sử dụng để đúc cả fungible token và non fungible token.

Còn tiêu chuẩn ERC-721 chỉ có thể sản xuất ra các non fungible token và buộc các nhà phát triển phải triển khai một hợp đồng thông minh mới cho mỗi token mới.

ERC-721 giống như việc bạn phải tạo ra một cái máy bán nước tự động cho một chai nước mới. Vô tình tạo ra nhiều sự lãng phí không những không gian, chi phí sản xuất mà còn thời gian phát triển khi triển khai NFT vào blockchain.

Do đó, dự liệu các token là cực kỳ không đồng nhất, hầu hết những dự án đều có cấu trúc dữ liệu khác nhau trong trong hợp đồng thông minh(smart contracts) của họ, điều này có nghĩa là nếu bạn muốn hỗ trợ ERC-721 từ nhiều dự án, bạn phải tạo tích hợp riêng cho mỗi token. Cuối cùng sẽ làm tốn thêm không gian và thời gian phát triển ứng dụng của bạn.

Và vì vậy mô hình phát triển cốt lõi của dữ liệu ERC-721 sẽ không thể mở rộng trong thị trường game và không thể phát triển trên quy môn lớn.

## Event TransferSingle
```
    /**
        event TransferSingle được emit khi chuyển 1 loại token
        `_operator` là địa chỉ (hay contract) có quyền thực hiện chuyển token (được `_from` ủy quyền) (`_operator` ở đây là msg.sender)
        `_from` là địa chỉ gửi token
        `_to` là địa chỉ nhận token
        `_id` loại token được chuyển
        `_value` lượng token được chuyển
        Với giao dịch tạo token, `_from` là địa chỉ `0x0`
        Với giao dịch hủy token, `_from` là địa chỉ `0x0`
    */
    event TransferSingle(
        address indexed _operator,
        address indexed _from,
        address indexed _to,
        uint256 _id,
        uint256 _value
    );
```

## Event TransferBatch
```
    /**
        event TransferBatch được emit khi chuyển nhiều loại token
        `_operator` là địa chỉ (hay contract) được phê duyệt để thực hiện chuyển khoản (msg.sender)
        `_from` là địa chỉ gửi token
        `_to` là địa chỉ nhận token
        `_ids` là danh sách các loại token được gửi
        `_values` là danh sách số lượng token được gửi (ứng với từng loại token trong tham số `_ids` ở trên)
        Với giao dịch tạo token, `_from` là địa chỉ `0x0`
        Với giao dịch hủy token, `_from` là địa chỉ `0x0`
    */
    event TransferBatch(
        address indexed _operator,
        address indexed _from,
        address indexed _to,
        uint256[] _ids,
        uint256[] _values
    );
```

## safeTransferFrom
```
    /**     
        Hàm thực hiện chuyển chuyển token
        revert nếu `_to` là địa chỉ `0x0`
        revert nếu số dư token bé hơn `_value`
        Emit event TransferSingle khi gửi
        @param _from    địa chỉ gửi
        @param _to      địa chủ nhận
        @param _id      ID của loại token
        @param _value   Số lượng token cần gửi
        @param _data    Additional data with no specified format, MUST be sent unaltered in call to `onERC1155Received` on `_to`
         Sau khi thỏa mãn các điều kiện tra, hàm sẽ kiểm tra xem địa chỉ `_to` có là địa chỉ      contract hay không (code size > 0) ?
        Nếu có thì phải gọi đến `onERC1155Received`  thuộc contract `_to`
    */
    function safeTransferFrom(
        address _from,
        address _to,
        uint256 _id,
        uint256 _value,
        bytes calldata _data
    ) external;
```

## safeBatchTransferFrom
```
    /**                  
        Hàm gửi nhiều loại Token
        revert nếu `_to` là địa chỉ `0x0`
        revert nếu độ dài mảng `_ids` khác độ dài mảng `_values`
        revert nếu có trường hợp số lượng token gửi đi lớn hơn số token hiện có
        emit event `TransferSingle` hoặc `TransferBatch` tùy vào số lượng token gửi đi
        @param _from    địa chỉ gửi
        @param _to      địa chỉ nhận
        @param _ids     Danh sách ID của các loại token cần gửi
        @param _values  Số lượng từng loại token tương ứng cần gửi
        @param _data    
        Sau khi thỏa mãn các điều kiện tra, hàm sẽ kiểm tra xem địa chỉ `_to` có là địa chỉ       contract hay không (code size > 0) ?
        Nếu có thì phải gọi đến `onERC1155Received` hoặc `onERC1155BatchReceived` thuộc contract `_to`
    */
    function safeBatchTransferFrom(
        address _from,
        address _to,
        uint256[] calldata _ids,
        uint256[] calldata _values,
        bytes calldata _data
    ) external;
```

## balanceOf
```
    /**
        Hàm trả về số lượng token hiện có của tài khoản
        @param _owner  địa chỉ cần kiểm tra
        @param _id     id của loại token
     */
    function balanceOf(address _owner, uint256 _id)
        external
        view
        returns (uint256);
```

## balanceOfBatch
```
    /**
        Hàm trả về số lượng token hiện có của nhiều tài khoản
        @param _owners Danh sách các địa chỉ
        @param _ids    Danh sách id của token
     */
    function balanceOfBatch(address[] calldata _owners, uint256[] calldata _ids)
        external
        view
        returns (uint256[] memory);
```

## setApprovalForAll
```
    /**
        Cho phép hoặc vô hiệu bên thứ 3 tham gia vào quá trình quản lý token
        emit event ApprovalForAll
        @param _operator  Địa chỉ được ủy quyền
        @param _approved  True là được ủy quyền, false là vô hiệu
    */
    function setApprovalForAll(address _operator, bool _approved) external;
```

## isApprovedForAll
```
    /**
        Truy vấn xem địa chỉ `_operator` có được ủy quyền với token của `_owner` không ?
        @param _owner     Chủ của token
        @param _operator  Địa chỉ được ủy quyền
       
    */
    function isApprovedForAll(address _owner, address _operator)
        external
        view
        returns (bool);
```

## onERC1155Received
```
    /**
        @notice Hàm sẽ được gọi khi contract được nhận 1 loại token (`safeTransferFrom`). 
        @notice Xử lý việc nhận 1 loại token ERC1155
        @param _operator  Địa chỉ (hay contract) được phê duyệt để thực hiện chuyển khoản (msg.sender)
        @param _from      Địa chỉ gửi token
        @param _id        ID của loại token
        @param _value     Lượng token cần gửi
        @param _data      Dữ liệu bổ sung (không có định dạng cụ thể)
        @return giá trị trả về: bytes4(keccak256("onERC1155Received(address,address,uint256,uint256,bytes)")
    */
    function onERC1155Received(address _operator, address _from, uint256 _id, uint256 _value, bytes calldata _data) external returns(bytes4);
```

## onERC1155BatchReceived
```
    /**
        @notice Hàm sẽ được gọi khi contract được nhận nhiều loại token (`safeBatchTransferFrom`).
        @param _operator  Địa chỉ (hay contract) được phê duyệt để thực hiện chuyển khoản (msg.sender)
        @param _from      Địa chỉ gửi token
        @param _ids       Danh sách ID của các loại token được gửi
        @param _values    Danh sách lượng token cần gửi tương ứng với mỗi loại
        @param _data      Dữ liệu bổ sung (không có định dạng cụ thể)
        @return giá trị trả về: `bytes4(keccak256("onERC1155BatchReceived(address,address,uint256[],uint256[],bytes)"))`
    */
    function onERC1155BatchReceived(address _operator, address _from, uint256[] calldata _ids, uint256[] calldata _values, bytes calldata _data) external returns(bytes4);  
```

# ChainLink

## Oracle
Oracle trong lĩnh vực Blockchain được hiểu là nguồn cấp dữ liệu, cho phép các dịch vụ của bên thứ ba cung cấp cho các hợp đồng thông minh những thông tin bên ngoài thế giới thực vào trong thế giới blockchain.

Ví dụ: Nếu hai bên đang đặt cược vào trò chơi bóng rổ thông qua hợp đồng thông minh trên blockchain, thì bên thứ ba là Oracle sẽ cho phép hợp đồng thông minh biết kết quả trận đấu bằng cách xuất bản dữ liệu liên quan lên blockchain. Quá trình này thường được tự động hóa bằng phần mềm. Một bot có thể quét NBA.com để biết điểm số của các trận đấu và tự động xuất bản chúng lên blockchain. Nhưng cho dù đó là một người hay phần mềm, nó vẫn tồn tại bên ngoài blockchain.

Chainlink đơn giản là một mạng oracle phi tập trung, đảm bảo sự tin cậy, toàn vẹn cho nguồn dữ liệu bên ngoài đưa vào blockchain qua các cơ chế đồng thuận. Mạng ChainLink bao gồm nhiều node (oracle), điều này tránh được việc 1 điểm lỗi duy nhất mà các oracle tập trung gặp phải.

![alt text](https://images.viblo.asia/a2e79af3-1d40-499d-bab4-b27ca19743a3.png)

Kiến trúc Chainlink gồm 2 phần chính:

- Phần thuộc blockchain (on-chain): User smart contract (User-SC), chainlink smartcontract (Chainlink-SC hay Oracle Contract).
- Phần bên ngoài mạng blockchain (off-chain): Chainlink Node (Oracle) và External API.

`User-SC`: Smart contract thông thường được viết bằng Solidity hay Vyper, chứa logic của ứng dụng.

`Oracle contract`: Smart contract trên Ethereum, được cung cấp bởi Oracle node. Oracle contract có nhiệm vụ nhận request từ user contract và chuyển đến các oracle node để xử lý tiếp.

`Chainlink Node`: Là các node trong mạng Chainlink, mỗi node sẽ có một phần core chứa logic hoạt động và phần adapter giúp lấy dữ liệu từ các API bên ngoài (get, post, ...)

`External API`: Là các trang web, dịch vụ lưu trữ dữ liệu bên ngoài.

# Chainlink VRF

Chainlink VRF là viết tắt của Chainlink Verifiable Random Function, là một liên kết đã được kiểm chứng và xác minh về tính ngẫu nhiên được sắp xếp chính xác cho các hợp đồng thông minh. Các nhà phát triển hợp đồng thông minh sử dụng Chainlink VRF để xây dựng những hợp đồng thông minh đáng tin cậy cho bất kì ứng dụng nào mà yêu cầu kết quả đầu ra ngẫu nhiên, ví dụ:
- Tạo ra các game đáng tin cậy hơn bằng cách sử dụng nguồn ngẫu nhiên có thể xác minh được trên chuỗi.
- Tạo ra các game vui hơn, thử thách hơn bằng cách tạo ra các thách thức và kịch bản, môi trường không dự đoán trước được, và đồng thời chỉ định phần thưởng cho người chơi một cách không thể dự đoán trước, như là một phần thưởng chiến lợi phẩm.
- Tạo ra các nhiệm vụ và tài nguyên được giao một cách ngẫu nhiên, có thể chứng mình được, ví dụ: chỉ định các thẩm phán một cách ngẫu nhiên cho các vụ việc hoặc kiểm toàn viên cho các công ty dưới sự giám sát kĩ lưỡng.
- Chọn một mẫu đại diện gồm các quan sát viên đủ điều kiện bỏ phiếu cho một đề xuất mà hợp đồng cần để thiết lập sự đồng thuận.

## Cách thức hoạt động của Chainlink VRF
Một hợp đồng thông minh yêu cầu một đối tượng ngẫu nhiên bằng cách cung cấp 1 seed phase cho Chainlink. Seed phase này không thể đoán trước được với các Oracle, nó được sử dụng để tạo ra một số ngẫu nhiên, sau đó được gửi đến hợp đồng thông minh trên chuỗi.

Mỗi oracle sử dụng khóa bị mật của riêng mình khi tạo ra đối tượng ngẫu nhiên này.

Khi kết quả được xuất bản trên chuỗi cùng với một bằng chứng, nó sẽ được xác minh bằng cách sử dụng khóa công khai của oracle và seed phase của ứng dụng.

Dựa vào khả năng xác minh bằng chứng và chữ kí được chấp nhận rộng rãi của một blockchain, điều này cho phép các hợp đồng chỉ sử dụng tính ngẫu nhiên cũng đã được xác minh bởi cùng một môi trường trên chuỗi đang chạy chính hợp đồng đó.
![alt text](https://coinf.io/wp-content/uploads/2021/11/chainlink-vrf-is-provably-fair-1024x430.png)
## Lợi ích của việc sử dụng Chainlink VRF
- Lợi ích cơ bản của việc sử dụng Chainlink VRF là tính ngẫu nhiên có thể kiểm chứng của nó. Ngay cả khi một nút bị xâm phạm, nó không thể thao tung hoặc cung cấp các câu trả lời sai lệch. Trường hợp xấu nhất là nút bị xâm phạm, không trả lại phản hồi cho một yêu cầu, nút này sẽ xuất hiện mãi mãi trên blockchain và không được tham gia vào việc cung cấp các bằng chứng xác thực sau này nữa.
- Một lợi ích bổ sung của Chainlink VRF là, khi nhiều người dùng sử dụng nó, phí người dùng phải trả cho các node tăng lên, tạo động lực cho các nhà khai thác nút cung cấp càng nhiều đảm bảo an ninh càng tốt. Chất lượng của các nút tăng lên càng tăng độ tin cậy cho người dùng sử dụng Chainlink VRF
## Ứng dụng của Chainlink VRF trong Gaming và NFT
### Phân phối các nhân vật
Hầu hết các game đều có nhiều nhân vật khác nhau, mỗi nhân vật lại có các thuộc tính riêng biệt. Một vài nhân vật phổ biến trong khi những nhân vật khác sẽ có độ hiếm khác nhau. Việc xác định cách mà các nhân vật được tạo ra là rất quan trọng để tạo ra một trò chơi công bằng, đặc biệt trong các game blockchain Play-to-earn khi mà người chơi kiếm được nhiều phần thưởng (tiền) hơn khi họ sở hữu các nhân vật tốt hơn.

Axie Infinity là một trong những game blockchain play-to-earn phổ biến, nơi mà người chơi sẽ chiến đấu, nâng cấp và giao dịch các nhân vật NFT gọi là các Axies. Mỗi Axie bao gồm 6 phần – lưng, tai, mắt, sừng miệng và đuôi, mỗi phần này lại có những thông số và đặc điểm khác nhau.

Bởi vì một số các đặc trưng sẽ có giá trị hơn những cái khác, nên Axie Infinity đã tích hợp với Chainlink VRF để chắc chắn rằng mỗi trong số 4088 Origin Axies được tạo ra sẽ có các đặc tính một cách ngẫu nhiên dựa trên tỷ lệ đã được định nghĩa sẵn trong hợp đồng thông minh của họ.
![alt text](https://coinf.io/wp-content/uploads/2021/11/axie-infinity-chainlink-vrf-1024x576.png)
### Ghép cặp người chơi trong các trận thi đấu PVP và Giải đấu
Việc ghép cặp người chơi là thành phần quan trọng của các trò chơi nhiều người chơi có tính năng thi đấu người với người (PVP). Sự thành công của người chơi và khả năng dành các phần thưởng của họ sẽ phụ thuộc nhiều vào đối thủ mà họ được ghép cặp trong các trận thi đấu, tạo ra sự quan trọng của việc ghép cặp một cách hợp lý.

CryptoBlades là một game blockchain nhập vai nơi người chơi có thể rèn các vật phẩm duy nhất, tiêu diệt quái vật, tham gia vào các cuộc đột kích và chiến đấu chống lại người chơi khác trong các trận thi đấu PvP.

Một trong nhiều cách mà CryptoBlades sử dụng Chainlink VRF là để thiết lập các cặp thi đấu không dự đoán trước, mà người thắng cuộc có thể dành các phần thưởng là token $SKILL. Nhờ sự công bằng của Chainlink VRF mà người chơi có thể yên tâm rằng sẽ không hề có một sự can thiệp nào đến việc ghép cặp này để tạo ra lợi ích cho một vài cá nhân/người chơi cụ thể.
### Game dựa trên sự may mắn
Một vài loại game lại dựa vào sự may mắn hơn là dựa vào khả năng của người chơi và kĩ năng của nhân vật mà họ điều khiển.

DeRace là một game mà người chơi thu thập, lai tạo và đua các chú ngựa NFT để giành phần thưởng chiến thắng. Thay vì mặc định rằng những chú ngựa có chỉ số cao sẽ chắc chắn giành chiến thắng trong mọi cuộc đua, DeRace tích hợp với Chainlink VRF để ngẫu nhiên tạo ra kết quả của cuộc đua.

Trước khi bắt đầu cuộc đua, hợp đồng thông minh sẽ so sánh chỉ số của mỗi chú ngựa tham gia và tính toán tỉ lệ thắng cuộc. Chainlink VRF sẽ lựa chọn ngẫu nhiên chú ngựa dành chiến thắng dựa trên các khả năng đó để đem lại nhiều sự hứng thú và khó dự đoán hơn. Điều này là hoàn toàn đúng trong các cuộc đua ngoài đời thực khi mà người chiến thắng rất khó để dự đoán.
### Nâng cấp nhân vật
Nâng cấp các nhân vật chắc chắn là một tính năng không thể thiếu trong hầu hết các trò chơi. Sau một quá trình tham gia và tích lũy kinh nghiệm, người chơi có các lựa chọn nâng cấp các nhân vật của mình. Mỗi quá trình nâng cấp thành công sẽ có cơ hội tạo ra các thuộc tính nâng cao. Và việc đảm bảo tính ngẫu nhiên của quá trình này là cần thiết để tạo ra một môi trường game công bằng.

### Tạo ra các bản đồ và các vật phẩm trong mỗi bản đồ
Trong khi nhiều game sẽ có các bản đồ cố định thì một số game lại có những thuật toán để tạo ra các vùng đất mới và nhiều tính năng khác nhau bên trong mỗi vùng đất đó. Tính ngẫu nhiên có thể được áp dụng vào các thuật toán này để lựa chọn trong 1 danh sách các đầu ra.

OVR là một trò chơi thực tế ảo mà người chơi có thể hợp nhất thế giới thực và thế giới ảo để mở khóa các kinh nghiệm duy nhất, và đạt được phần thưởng ở những vị trí khác nhau.

Thế giới ảo OVR được chia thành 300 OVRLand NFT diễn tả cho 300 mét vuông trong thế giới thực. Chủ sỡ hữu của những NFT này có thể tùy chỉnh kinh nghiệm và mô phỏng cho những đối thủ khác của mình. Đồng thời, người chơi có thể bắt gặp các rương kho báu và các sự kiện độc đáo khác khi họ khám phá metaverse.

OVR sử dụng Chainlink VRF để ngẫu nhiễn tạo ra các chương kho báu ở các vị trí khác nhau trong các OVRLand, giúp tạo ra một vùng đất hoàn toàn khác với các vùng đất khác, đem đến cơ hội công bằng cho tất cả các người chơi.
### Xác định thứ tự thi đấu
Một trong những game đầu tiên trên Avalanche blockchain là Avaxcells – NFT game card mà người chơi có thể sử dụng để chiến đầu 1v1 với người chơi khác. Mỗi một Avaxcell NFT được đúc ra từ 1 trong 8 thành phần đặc biệt, như lửa, nước và gió, có những ưu thế và bất lợi độc nhất đối với các thành phần khác. Mỗi thẻ cũng có các đặc trưng về độ quý hiếm như phổ thông, đặc biệt, hiếm, sử thi và huyền thoại, xác định độ mạnh và hiếm của NFT.

Avaxcells tích hợp Chainlink VRF để xác định một cách công bằng người chơi nào sẽ được tất công trước trong các trận đấu PvP.
### Vị trí hồi sinh nhân vật
Khi một người chơi bị chết trong các trò chơi bắn súng, họ sẽ được hồi sinh sau đó ở một ví trí nào đó trên bản đồ, thông thường ở 1 vài vị trí cố định. Mặt khác, nếu người chơi được hồi sinh ở các vị trí khác nhau sẽ ảnh hưởng đến ưu thế hay bất lợi đối với người chơi đó, tùy vào vị trí mà họ được hồi sinh.

Trong các trò chơi bắn súng góc nhìn thứ nhất như Arsenal, việc sắp xếp nhân vật là một quá trình phức tạp nổi tiếng, vì những game thủ có kinh nghiệm hơn có thể ghi nhớ vị trí các điểm xuất hiện của các nhân vật sau khi chết, và họ sẽ chờ sẵn ở các điểm này để tấn công người chơi ngay khi họ hồi sinh.

Vì đây là một trò chơi năng động không cạnh tranh, Arsenal đang tích hợp với Chainlink VRF để đảm bảo rằng vị trí các nhân vật và điểm xuất phát của họ là tùy ý và khó đoán trước.
### Gán các thông số cho NFT sử dụng tính xác suất
Tương tự như Axie Infinity, NFTs thường được tạo ra với 1 số các thông số ngẫu nhiên từ 1 loạt các thuộc tính. Ví dụ như Polychain Monsters là 1 game blockchain, là nơi sinh sống của các quái vật dựa trên NFT với ba loại đặc điểm riêng biệt – màu sắc, loại sừng, và ánh kim, – và một số đặc điểm với độ hiếm khác nhau trong mỗi danh mục.

Sự kết hợp của các đặc điểm trên cả ba loại sẽ xác định độ hiếm của một Polychain Monster.

Độ hiếm của các Polychain Monster sẽ quyết định sức mạnh trong các trận chiến, vì vậy mà sự công bằng về tính ngẫu nhiên rất quan trọng trong quá trình tạo ra các Polychain Monster NFT.

Việc tích hợp với Chainlink VRF sẽ đảm bảo tính công bằng và ngẫu nhiên này.
Những đặc điểm này không chỉ áp dụng cho các nhân vật trong trò chơi, mà còn có thể áp dụng cho các đặc điểm của nghệ thuật. CryptOrchids là một dự án nghệ thuật mà các NFT có đặc điểm động., nơi các NFT có thể thay đổi theo thời gian để phản ánh sự phát triển trong thế giới thực.

Người dùng cần tưới nước cho CryptOrchids của họ hàng tuần trong khoảng thời gian 3 giờ cụ thể, nếu không hoa NFT của họ sẽ chết.

CryptOrchids sử dụng Chinlink VRF để xác định loài hoa NFT được đúc, với mỗi giống hoa sẽ có một độ hiếm nhất định. Loại hoa Shenzhen Nongke Orchid có tỉ lệ 1/10,000 cơ hội được đúc ra. Tuy nhiên, việc sử dụng xác suất vẫn có thể có nhiều hơn một giống này được đúc ra.

### Trao giải thưởng cho các NFT Holders
NFT cũng có thể đại diện cho quyền truy cập độc quyền vào các giải thưởng và phần thưởng trong thế giới thực, nơi chỉ những người nắm giữ NFT mới đủ điều kiện giành chiến thắng.

Thông qua quan hệ đối tác với Ether Cards, LaMelo Ball đã trở thành một trong những vận động viên chuyên nghiệp đầu tiên cung cấp thẻ giao dịch NFT cho người hâm mộ của mình.

Cấp cao nhất trong bản phát hành NFT của anh ấy, thẻ Gold Evolve, tự động đưa người sở hữu vào các đợt rút thăm ngẫu nhiên để giành được các kỷ vật như giày trong trò chơi, tay áo tùy chỉnh và nhẫn vô địch trường trung học của anh ấy

Bộ sưu tập NFT của LaMelo đã sử dụng Chainlink VRF để chọn người chiến thắng trong các đợt rút thăm này và sử dụng orcale Chainlink để đúc các NFT đặc biệt tùy thuộc vào việc anh ta có giành được giải thưởng Tân binh NBA năm 2021 hay không. LaMelo đã giành chiến thắng và Chainlink oracle đã cung cấp kết quả trực tuyến để kích hoạt giải thưởng Rookie of the Year NFT cho những người nắm giữ Gold Evolve.

Kể từ khi tích hợp Chainlink VRF, Ether Cards đã đạt được tổng doanh số hơn 24 triệu đô la, bao gồm hơn 6K + NFT duy nhất được mua.
## Chainlink VRF sample code
### Thêm Polygon Testnet vào Metamask
- Network Name: Polygon Testnet
- New RPC URL: https://rpc-mumbai.matic.today/
- Chain ID: 80001.
- Currency Symbol: MATIC.
- Block Explorer URL: https://explorer-mumbai.maticvigil.com/
### Import LINK token vào ví
- Address: 0x326C977E6efc84E512bB9C30f76E30c160eD06FB
### Claim MATIC token va LINK token
- https://faucet.polygon.technology/
### Tạo sample code
```
// SPDX-License-Identifier: MIT
pragma solidity 0.6.6;

import "@chainlink/contracts/src/v0.6/VRFConsumerBase.sol";

contract RandomNumber is VRFConsumerBase {
    bytes32 internal keyHash;
    uint256 internal fee;
    
    uint256 public randomResult;
    bytes32 public request;
    
    /**
     * Constructor inherits VRFConsumerBase
     * 
     * Network: Polygon (Matic) Mumbai Testnet
     * Chainlink VRF Coordinator address: 0x8C7382F9D8f56b33781fE506E897a4F1e2d17255
     * LINK token address:                0x326C977E6efc84E512bB9C30f76E30c160eD06FB
     * Key Hash: 0x6e75b569a01ef56d18cab6a8e71e6600d6ce853834d4a5748b720d06f878b3a4
     */
    constructor() 
        VRFConsumerBase(
            0x8C7382F9D8f56b33781fE506E897a4F1e2d17255, // VRF Coordinator
            0x326C977E6efc84E512bB9C30f76E30c160eD06FB  // LINK Token
        ) public
    {
        keyHash = 0x6e75b569a01ef56d18cab6a8e71e6600d6ce853834d4a5748b720d06f878b3a4;
        fee = 0.0001 * 10 ** 18; // 0.0001 LINK
    }
    
    /** 
     * Requests randomness 
     */
    function getRandomNumber() public returns (bytes32 requestId) {
        require(LINK.balanceOf(address(this)) > fee, "Not enough LINK - fill contract with faucet");
        return requestRandomness(keyHash, fee);
    }

    /**
     * Callback function used by VRF Coordinator
     */
    function fulfillRandomness(bytes32 requestId, uint256 randomness) internal override {
        request = requestId;
        randomResult = randomness;
    }
}
```
- Deploy trên Remix
1. Thực hiện getRandomNumber() sẽ báo lỗi vì khi thực hiện random sẽ mất phí LINK, nên cần transfer LINK vào contract.
2. Copy address của contract sau khi được deploy, quay trở lại Metamask transfer một lượng LINK vào contract.
3. Thực hiện getRandomNumber() lại lần nữa, lấy ra giá trị randomResult sẽ được: 91140232136701889567811469737095454324173320225978079664039634614108471846250

Nguồn: 
  https://coinf.io/chainlink-vrf-la-gi/#ftoc-heading-4
