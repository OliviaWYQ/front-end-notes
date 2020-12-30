# React Native Notes

## concat strings

1. 
f(){
   const apple = 'apple'
   const banana = 'banana'
   return apple + ' ' + banana
}

2. a safer function
f(){
   const apple = 'apple'
   const banana = 'banana'
   return `{$apple} {$banana}`
}

## synchronously and unsynchrously update in setState 

use setTimeout to make setState a synchronous function

```
setTimeout(() => {
   this.setState({
       state: data
   })
})
```

## Lazy init 

basical init
```
const contentTitle: string | undefined = undefined
const contentImage: string | undefined = undefined
const provider: Provider | undefined = undefined
const labWorkoutSummary: ActivitySessionLabWorkoutState = { contentTitle, contentImage, provider }
const [content, setContent] = useState(labWorkoutSummary)
```
v.s. lazy init
```  
const initialState = {} as ActivitySessionLabWorkoutState
const [content, setContent] = useState(initialState)
```
