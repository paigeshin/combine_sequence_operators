### min & max

```swift
import UIKit
import Combine

let publisher = [1, -45, 3, 45, 100].publisher

publisher
    .min()
    .sink {
        print($0) //-1
    }

publisher
    .max()
    .sink {
        print($0) //100 
    }
```

### First

```swift
import UIKit
import Combine

let publisher = ["A", "B", "C", "D"].publisher

publisher
    .first()
    .sink {
        print($0) // A
    }

publisher
    .first(where: { "Cat".contains($0) })
    .sink {
        print($0) // C
    }
```

### Last

```swift
import UIKit
import Combine

let publisher = ["A", "B", "C", "D"].publisher

publisher
    .last()
    .sink {
        print($0) // D
    }

publisher
    .last(where: { "Cat".contains($0) })
    .sink {
        print($0) // C
    }
```

### output

```swift
import UIKit
import Combine

let publisher = ["A", "B", "C", "D"].publisher

publisher
    .output(at: 2)
    .sink {
        print($0) // C
    }

publisher
    .output(in: (0...2))
    .sink {
        print($0) // A, B, C
    }
```

### count

```swift
import UIKit
import Combine

let publisher = ["A", "B", "C", "D"].publisher

publisher
    .count()
    .sink {
        print($0) // 4
    }
```

### completion event

```swift
import UIKit
import Combine

let publisher = PassthroughSubject<Int, Never>()

publisher
    .count()
    .sink {
        print($0) // 4, `publisher.send(completion: .finished)` 
    }

publisher.send(10) // this alone doesn't trigger anything
publisher.send(10) // this alone doesn't trigger anything
publisher.send(10) // this alone doesn't trigger anything
publisher.send(10) // this alone doesn't trigger anything
publisher.send(completion: .finished) // should call 'finished' event
```

### contains

```swift
import UIKit
import Combine

let publisher = ["A", "B", "C", "D"].publisher

publisher
    .contains("C")
    .sink {
        print($0) //true 
    }
```

### allSatisfy

```swift
import UIKit
import Combine

let publisher = [1, 2, 3, 4, 5, 6, 7].publisher

publisher
    .allSatisfy { $0 % 2 == 0 }
    .sink { allEven in
        print(allEven) //false 
    }
```

### reduce

```swift
import UIKit
import Combine

let publisher = [1, 2, 3, 4, 5, 6, 7].publisher

publisher
    .reduce(0) { acc, value in
        print("accumulator: \(acc) and the value is \(value)")
        return acc + value
    }
    .sink {
        print($0) // 28 
    }
```
