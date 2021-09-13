## Setup node
```
brazil-setup --node
Node 16.x path (i.e the path of node executable)
[?]:
Node 14.x path (i.e the path of node executable)
[?]:
Node 12.x path (i.e the path of node executable)
[?]: /usr/local/Cellar/node@12/12.22.5/bin/node
Node 10.x path (i.e the path of node executable)
[?]:
Node 8.x path (i.e the path of node executable)
[?]:
Node 6.x path (i.e the path of node executable)
[?]:
Node other path (i.e the path of node executable)
[?]: 

vim ~/.bash_profile
export PATH="/usr/local/Cellar/node@12/12.22.5/bin:$PATH"
source ~/.bash_profile
```

## Test all files
```
npx jest
```

Test single file, will transfer .ts or .js
```
jest + <path to the file>
```

Example:
```
import * as Network from 'axle-react-native-platform/lib/native_modules/Network'
import { jestMockFunction } from 'axle-slac-react-native-platform/lib/utils/test-utils'
import { AppStateStatus } from 'react-native'
 
jest.mock('react-native', () => {
     return {
         AppState: {
             currentState: <AppStateStatus>'active'
         }
     }
 })
 
 jest.mock('axle-react-native-platform/lib/native_modules/Network', () => {
     return {
         getNetworkStatus: jest.fn()
     }
 })
  
 
 describe('test yyy', () => {
     beforeEach(() => {
         jest.resetAllMocks()
     })
 
     it('yyy should return zzz', async () => {
         ;(Network.getNetworkStatus as jest.Mock<typeof Network.getNetworkStatus>).mockResolvedValueOnce({
             type: { name: 'WiFi' },
             isInternetReachable: true
         })
         jestMockFunction(xxx).mockImplementation(() => {
             return {
                 xxx
             }
         })
         expect(yyy).toBe(zzz)
     }
 }
 ```
