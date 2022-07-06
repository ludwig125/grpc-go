# references

https://docs.microsoft.com/ja-jp/aspnet/core/grpc/performance?view=aspnetcore-6.0
https://future-architect.github.io/articles/20220623a/
https://zenn.dev/hsaki/books/golang-grpc-starting/viewer/clientinterceptor
https://grpc.io/docs/languages/go/quickstart/
https://developers.google.com/protocol-buffers/docs/proto3#simple
https://github.com/golang/protobuf/
https://qiita.com/Captain_Blue/items/b7a1f4a42f48559fac0c
https://cyberbotics.com/doc/reference/proto-example
https://developers.google.com/protocol-buffers/docs/gotutorial
https://github.com/grpc/grpc-go/tree/master/examples/route_guide
https://pkg.go.dev/google.golang.org/grpc#section-readme
https://grpc.io/docs/languages/go/basics/

# install

https://grpc.io/docs/protoc-installation/

```
$sudo apt install -y protobuf-compiler

$protoc --version  # Ensure compiler version is 3+
libprotoc 3.6.1
```

# tutorial go

https://grpc.io/docs/languages/go/quickstart/

```
git clone -b v1.46.0 --depth 1 https://github.com/grpc/grpc-go
```

この helloworld を使う

```
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $go run greeter_server/main.go
2022/07/02 06:55:00 server listening at [::]:50051
2022/07/02 06:55:07 Received: world

```

```
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $go run greeter_client/main.go
2022/07/02 06:55:07 Greeting: Hello world
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $
```

https://grpc.io/docs/languages/go/quickstart/#update-the-grpc-service
に従って、proto ファイルを修正

```
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $protoc --go_out=. --go_opt=paths=source_relative \
    --go-grpc_out=. --go-grpc_opt=paths=source_relative \
    helloworld/helloworld.proto
```

server と client の import 先を自分のディレクトリに修正

```go
	// pb "google.golang.org/grpc/examples/helloworld/helloworld"
	pb "github.com/ludwig125/grpc-go/helloworld/helloworld"
```

server

```
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $go run greeter_server/main.go
2022/07/02 07:07:09 server listening at [::]:50051
2022/07/02 07:07:13 Received: world
```

client

```
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $go run greeter_client/main.go
2022/07/02 07:07:13 Greeting: Hello world
2022/07/02 07:07:13 Greeting: Hello again world
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $

[~/go/src/github.com/ludwig125/grpc-go/helloworld] $go run greeter_client/main.go --name=Alice
2022/07/02 07:09:17 Greeting: Hello Alice
2022/07/02 07:09:17 Greeting: Hello again Alice
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $
```

# official tutorial route_guide

https://grpc.io/docs/languages/go/basics/

https://github.com/grpc/grpc-go/tree/master/examples/route_guide
をローカルにコピー

```
[~/go/src/github.com/ludwig125/grpc-go/route_guide] $ protoc --go_out=. --go_opt=paths=source_relative \
    --go-grpc_out=. --go-grpc_opt=paths=source_relative \
    routeguide/route_guide.proto
```

```
[~/go/src/github.com/ludwig125/grpc-go/route_guide] $go run server/server.go
```

```
[~/go/src/github.com/ludwig125/grpc-go/route_guide] $go run client/client.go
2022/07/07 05:44:40 Getting feature for point (409146138, -746188906)
2022/07/07 05:44:40 name:"Berkshire Valley Management Area Trail, Jefferson, NJ, USA" location:{latitude:409146138 longitude:-746188906}
2022/07/07 05:44:40 Getting feature for point (0, 0)
2022/07/07 05:44:40 location:{}
2022/07/07 05:44:40 Looking for features within lo:{latitude:400000000 longitude:-750000000} hi:{latitude:420000000 longitude:-730000000}
2022/07/07 05:44:40 Feature: name: "Patriots Path, Mendham, NJ 07945, USA", point:(407838351, -746143763)
2022/07/07 05:44:40 Feature: name: "101 New Jersey 10, Whippany, NJ 07981, USA", point:(408122808, -743999179)
2022/07/07 05:44:40 Feature: name: "U.S. 6, Shohola, PA 18458, USA", point:(413628156, -749015468)
2022/07/07 05:44:40 Feature: name: "5 Conners Road, Kingston, NY 12401, USA", point:(419999544, -740371136)
2022/07/07 05:44:40 Feature: name: "Mid Hudson Psychiatric Center, New Hampton, NY 10958, USA", point:(414008389, -743951297)
2022/07/07 05:44:40 Feature: name: "287 Flugertown Road, Livingston Manor, NY 12758, USA", point:(419611318, -746524769)
2022/07/07 05:44:40 Feature: name: "4001 Tremley Point Road, Linden, NJ 07036, USA", point:(406109563, -742186778)
2022/07/07 05:44:40 Feature: name: "352 South Mountain Road, Wallkill, NY 12589, USA", point:(416802456, -742370183)
2022/07/07 05:44:40 Feature: name: "Bailey Turn Road, Harriman, NY 10926, USA", point:(412950425, -741077389)
2022/07/07 05:44:40 Feature: name: "193-199 Wawayanda Road, Hewitt, NJ 07421, USA", point:(412144655, -743949739)
2022/07/07 05:44:40 Feature: name: "406-496 Ward Avenue, Pine Bush, NY 12566, USA", point:(415736605, -742847522)
2022/07/07 05:44:40 Feature: name: "162 Merrill Road, Highland Mills, NY 10930, USA", point:(413843930, -740501726)
2022/07/07 05:44:40 Feature: name: "Clinton Road, West Milford, NJ 07480, USA", point:(410873075, -744459023)
2022/07/07 05:44:40 Feature: name: "16 Old Brook Lane, Warwick, NY 10990, USA", point:(412346009, -744026814)
2022/07/07 05:44:40 Feature: name: "3 Drake Lane, Pennington, NJ 08534, USA", point:(402948455, -747903913)
2022/07/07 05:44:40 Feature: name: "6324 8th Avenue, Brooklyn, NY 11220, USA", point:(406337092, -740122226)
2022/07/07 05:44:40 Feature: name: "1 Merck Access Road, Whitehouse Station, NJ 08889, USA", point:(406421967, -747727624)
2022/07/07 05:44:40 Feature: name: "78-98 Schalck Road, Narrowsburg, NY 12764, USA", point:(416318082, -749677716)
2022/07/07 05:44:40 Feature: name: "282 Lakeview Drive Road, Highland Lake, NY 12743, USA", point:(415301720, -748416257)
2022/07/07 05:44:40 Feature: name: "330 Evelyn Avenue, Hamilton Township, NJ 08619, USA", point:(402647019, -747071791)
2022/07/07 05:44:40 Feature: name: "New York State Reference Route 987E, Southfields, NY 10975, USA", point:(412567807, -741058078)
2022/07/07 05:44:40 Feature: name: "103-271 Tempaloni Road, Ellenville, NY 12428, USA", point:(416855156, -744420597)
2022/07/07 05:44:40 Feature: name: "1300 Airport Road, North Brunswick Township, NJ 08902, USA", point:(404663628, -744820157)
2022/07/07 05:44:40 Feature: name: "", point:(407113723, -749746483)
2022/07/07 05:44:40 Feature: name: "", point:(402133926, -743613249)
2022/07/07 05:44:40 Feature: name: "", point:(400273442, -741220915)
2022/07/07 05:44:40 Feature: name: "", point:(411236786, -744070769)
2022/07/07 05:44:40 Feature: name: "211-225 Plains Road, Augusta, NJ 07822, USA", point:(411633782, -746784970)
2022/07/07 05:44:40 Feature: name: "", point:(415830701, -742952812)
2022/07/07 05:44:40 Feature: name: "165 Pedersen Ridge Road, Milford, PA 18337, USA", point:(413447164, -748712898)
2022/07/07 05:44:40 Feature: name: "100-122 Locktown Road, Frenchtown, NJ 08825, USA", point:(405047245, -749800722)
2022/07/07 05:44:40 Feature: name: "", point:(418858923, -746156790)
2022/07/07 05:44:40 Feature: name: "650-652 Willi Hill Road, Swan Lake, NY 12783, USA", point:(417951888, -748484944)
2022/07/07 05:44:40 Feature: name: "26 East 3rd Street, New Providence, NJ 07974, USA", point:(407033786, -743977337)
2022/07/07 05:44:40 Feature: name: "", point:(417548014, -740075041)
2022/07/07 05:44:40 Feature: name: "", point:(410395868, -744972325)
2022/07/07 05:44:40 Feature: name: "", point:(404615353, -745129803)
2022/07/07 05:44:40 Feature: name: "611 Lawrence Avenue, Westfield, NJ 07090, USA", point:(406589790, -743560121)
2022/07/07 05:44:40 Feature: name: "18 Lannis Avenue, New Windsor, NY 12553, USA", point:(414653148, -740477477)
2022/07/07 05:44:40 Feature: name: "82-104 Amherst Avenue, Colonia, NJ 07067, USA", point:(405957808, -743255336)
2022/07/07 05:44:40 Feature: name: "170 Seven Lakes Drive, Sloatsburg, NY 10974, USA", point:(411733589, -741648093)
2022/07/07 05:44:40 Feature: name: "1270 Lakes Road, Monroe, NY 10950, USA", point:(412676291, -742606606)
2022/07/07 05:44:40 Feature: name: "509-535 Alphano Road, Great Meadows, NJ 07838, USA", point:(409224445, -748286738)
2022/07/07 05:44:40 Feature: name: "652 Garden Street, Elizabeth, NJ 07202, USA", point:(406523420, -742135517)
2022/07/07 05:44:40 Feature: name: "349 Sea Spray Court, Neptune City, NJ 07753, USA", point:(401827388, -740294537)
2022/07/07 05:44:40 Feature: name: "13-17 Stanley Street, West Milford, NJ 07480, USA", point:(410564152, -743685054)
2022/07/07 05:44:40 Feature: name: "47 Industrial Avenue, Teterboro, NJ 07608, USA", point:(408472324, -740726046)
2022/07/07 05:44:40 Feature: name: "5 White Oak Lane, Stony Point, NY 10980, USA", point:(412452168, -740214052)
2022/07/07 05:44:40 Feature: name: "Berkshire Valley Management Area Trail, Jefferson, NJ, USA", point:(409146138, -746188906)
2022/07/07 05:44:40 Feature: name: "1007 Jersey Avenue, New Brunswick, NJ 08901, USA", point:(404701380, -744781745)
2022/07/07 05:44:40 Feature: name: "6 East Emerald Isle Drive, Lake Hopatcong, NJ 07849, USA", point:(409642566, -746017679)
2022/07/07 05:44:40 Feature: name: "1358-1474 New Jersey 57, Port Murray, NJ 07865, USA", point:(408031728, -748645385)
2022/07/07 05:44:40 Feature: name: "367 Prospect Road, Chester, NY 10918, USA", point:(413700272, -742135189)
2022/07/07 05:44:40 Feature: name: "10 Simon Lake Drive, Atlantic Highlands, NJ 07716, USA", point:(404310607, -740282632)
2022/07/07 05:44:40 Feature: name: "11 Ward Street, Mount Arlington, NJ 07856, USA", point:(409319800, -746201391)
2022/07/07 05:44:40 Feature: name: "300-398 Jefferson Avenue, Elizabeth, NJ 07201, USA", point:(406685311, -742108603)
2022/07/07 05:44:40 Feature: name: "43 Dreher Road, Roscoe, NY 12776, USA", point:(419018117, -749142781)
2022/07/07 05:44:40 Feature: name: "Swan Street, Pine Island, NY 10969, USA", point:(412856162, -745148837)
2022/07/07 05:44:40 Feature: name: "66 Pleasantview Avenue, Monticello, NY 12701, USA", point:(416560744, -746721964)
2022/07/07 05:44:40 Feature: name: "", point:(405314270, -749836354)
2022/07/07 05:44:40 Feature: name: "", point:(414219548, -743327440)
2022/07/07 05:44:40 Feature: name: "565 Winding Hills Road, Montgomery, NY 12549, USA", point:(415534177, -742900616)
2022/07/07 05:44:40 Feature: name: "231 Rocky Run Road, Glen Gardner, NJ 08826, USA", point:(406898530, -749127080)
2022/07/07 05:44:40 Feature: name: "100 Mount Pleasant Avenue, Newark, NJ 07104, USA", point:(407586880, -741670168)
2022/07/07 05:44:40 Feature: name: "517-521 Huntington Drive, Manchester Township, NJ 08759, USA", point:(400106455, -742870190)
2022/07/07 05:44:40 Feature: name: "", point:(400066188, -746793294)
2022/07/07 05:44:40 Feature: name: "40 Mountain Road, Napanoch, NY 12458, USA", point:(418803880, -744102673)
2022/07/07 05:44:40 Feature: name: "", point:(414204288, -747895140)
2022/07/07 05:44:40 Feature: name: "", point:(414777405, -740615601)
2022/07/07 05:44:40 Feature: name: "48 North Road, Forestburgh, NY 12777, USA", point:(415464475, -747175374)
2022/07/07 05:44:40 Feature: name: "", point:(404062378, -746376177)
2022/07/07 05:44:40 Feature: name: "", point:(405688272, -749285130)
2022/07/07 05:44:40 Feature: name: "", point:(400342070, -748788996)
2022/07/07 05:44:40 Feature: name: "", point:(401809022, -744157964)
2022/07/07 05:44:40 Feature: name: "9 Thompson Avenue, Leonardo, NJ 07737, USA", point:(404226644, -740517141)
2022/07/07 05:44:40 Feature: name: "", point:(410322033, -747871659)
2022/07/07 05:44:40 Feature: name: "", point:(407100674, -747742727)
2022/07/07 05:44:40 Feature: name: "213 Bush Road, Stone Ridge, NY 12484, USA", point:(418811433, -741718005)
2022/07/07 05:44:40 Feature: name: "", point:(415034302, -743850945)
2022/07/07 05:44:40 Feature: name: "", point:(411349992, -743694161)
2022/07/07 05:44:40 Feature: name: "1-17 Bergen Court, New Brunswick, NJ 08901, USA", point:(404839914, -744759616)
2022/07/07 05:44:40 Feature: name: "35 Oakland Valley Road, Cuddebackville, NY 12729, USA", point:(414638017, -745957854)
2022/07/07 05:44:40 Feature: name: "", point:(412127800, -740173578)
2022/07/07 05:44:40 Feature: name: "", point:(401263460, -747964303)
2022/07/07 05:44:40 Feature: name: "", point:(412843391, -749086026)
2022/07/07 05:44:40 Feature: name: "", point:(418512773, -743067823)
2022/07/07 05:44:40 Feature: name: "42-102 Main Street, Belford, NJ 07718, USA", point:(404318328, -740835638)
2022/07/07 05:44:40 Feature: name: "", point:(419020746, -741172328)
2022/07/07 05:44:40 Feature: name: "", point:(404080723, -746119569)
2022/07/07 05:44:40 Feature: name: "", point:(401012643, -744035134)
2022/07/07 05:44:40 Feature: name: "", point:(404306372, -741079661)
2022/07/07 05:44:40 Feature: name: "", point:(403966326, -748519297)
2022/07/07 05:44:40 Feature: name: "", point:(405002031, -748407866)
2022/07/07 05:44:40 Feature: name: "", point:(409532885, -742200683)
2022/07/07 05:44:40 Feature: name: "", point:(416851321, -742674555)
2022/07/07 05:44:40 Feature: name: "3387 Richmond Terrace, Staten Island, NY 10303, USA", point:(406411633, -741722051)
2022/07/07 05:44:40 Feature: name: "261 Van Sickle Road, Goshen, NY 10924, USA", point:(413069058, -744597778)
2022/07/07 05:44:40 Feature: name: "", point:(418465462, -746859398)
2022/07/07 05:44:40 Feature: name: "", point:(411733222, -744228360)
2022/07/07 05:44:40 Feature: name: "3 Hasta Way, Newton, NJ 07860, USA", point:(410248224, -747127767)
2022/07/07 05:44:40 Traversing 59 points.
2022/07/07 05:44:40 Route summary: point_count:59 distance:541001578
2022/07/07 05:44:40 Got message First message at point(0, 1)
2022/07/07 05:44:40 Got message Second message at point(0, 2)
2022/07/07 05:44:40 Got message Third message at point(0, 3)
2022/07/07 05:44:40 Got message First message at point(0, 1)
2022/07/07 05:44:40 Got message Fourth message at point(0, 1)
2022/07/07 05:44:40 Got message Second message at point(0, 2)
2022/07/07 05:44:40 Got message Fifth message at point(0, 2)
2022/07/07 05:44:40 Got message Third message at point(0, 3)
2022/07/07 05:44:40 Got message Sixth message at point(0, 3)
[~/go/src/github.com/ludwig125/grpc-go/route_guide] $
```

# sample

https://developers.google.com/protocol-buffers/docs/gotutorial

protoc

- ref: https://zenn.dev/hsaki/books/golang-grpc-starting/viewer/codegenerate
- https://grpc.io/docs/languages/go/quickstart/
