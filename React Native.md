# React Native Notes

## PanResponder and TouchableOpacity
How to catch the panResponder move event as well as the inner component touch event

```
    topViewResponder = PanResponder.create({
        onStartShouldSetPanResponder: () => true,
        onMoveShouldSetPanResponder: (_evt, _gestureState) => {
            // If the user is swiping, return true and use topViewPanResponder; if it's a single click, return false and use inner touchable components
            return Math.abs(_gestureState.dx) > 2 || Math.abs(_gestureState.dy) > 2;
        },
        onPanResponderGrant: (_evt, _gestureState) => {},
        onPanResponderMove: (_evt, _gestureState) => {},
        onPanResponderRelease: (_evt, _gestureState) => {}
    })

```

## two-way data transfer

1. get state from BiometricDetailsMembershipGatedHeaderContent, and transfer it to BiometricDetailPage.
2. use props to transfer ActivityMembershipUpsellModal as a whole component to BiometricDetailsMembershipGatedHeaderContent
3. update state inside ActivityMembershipUpsellModal from the parent stateshowModal when clicking 'SEE MEMEBERSHIP BENEFIT' button or 'Close' button

AxleAppReactNative: src/pages/BiometricDetailPage/BiometricDetailPage.tsx

```
 // transfer showModal state from AxleSlacReactNativePlatform
     let setShowModalPointer: React.Dispatch<React.SetStateAction<boolean>>
     const [showMembershipUpsellModal, setShowMembershipUpsellModal] = useState<boolean>(false)
     const onCloseMembershipUpsellModal = useCallback(
         () => {
             setShowMembershipUpsellModal(false)
             setShowModalPointer(false)
         },
         [setShowMembershipUpsellModal]
     )
  
     const upsellModalHandler = (showModal: boolean, setShowModal: React.Dispatch<React.SetStateAction<boolean>>) => {
         setShowModalPointer = setShowModal
         useEffect(
             () => {
                 setShowMembershipUpsellModal(showModal)
             },
             [showModal]
         )
     }
  
     return (
         <SlacBiometricDetailPageLayoutWithGraphQueryless
             // tslint:disable-next-line
             upsellModalInfo={upsellModalHandler.bind(this)}
             customizedMembershipUpsellModalComponent={
                 <ActivityMembershipUpsellModal
                     testID={'activity-biometric-detail-membership-upsell-modal'}
                     onCloseModal={onCloseMembershipUpsellModal}
                     visible={showMembershipUpsellModal}
                 />
             }
         />
     )
 }

```

AxleSlacReactNativePlatform: src/components/biometric-detail-page/components/BiometricDetailsMembershipGatedHeader.tsx

```
     const [showModal, setShowModal] = useState<boolean>(false)
     const onLockButtonPress = useCallback(
         () => {
             setShowModal(true)
         },
         [showModal, setShowModal]
     )
     const showMembershipUpsellModal = () => {
         if (props.customizedMembershipUpsellModalComponent && props.upsellModalInfo) {
             props.upsellModalInfo(showModal, setShowModal)
             return props.customizedMembershipUpsellModalComponent
         } else {
             return null
         }
     }
     return (
          <View>
             <BiometricDetailsMembershipGatedHeaderContent
                 onLockButtonPress={onLockButtonPress}
             />
             {showMembershipUpsellModal()}
         </View>
     )
 }
```

AxleSlacReactNativePlatform: src/components/biometric-detail-page/SlacBiometricDetailPageLayoutWithGraphQueryless.tsx

```
/**
  *  types passing from customized membership upsell modal
  */
 export interface SlacBiometricDetailPageMembershipUpsellModalProps {
     upsellModalInfo?: (showModal: boolean, setShowModal: React.Dispatch<React.SetStateAction<boolean>>) => void
     customizedMembershipUpsellModalComponent?: JSX.Element
 }

...
...
...

            valueSection = (
                 <BiometricDetailsMembershipGatedHeader
                     upsellModalInfo={this.props.upsellModalInfo}
                     customizedMembershipUpsellModalComponent={this.props.customizedMembershipUpsellModalComponent}
                     {...this.props.membershipHeaderProps}
                     currentMembershipStatus={this.props.currentMembershipStatus}
                     historicalMembershipStatus={this.props.biometricHistoricalMembershipStatus}
                 />
             )
```


## concat strings

1. 
```
f(){
   const apple = 'apple'
   const banana = 'banana'
   return apple + ' ' + banana
}
```

2. 
```
f(){
   const apple = 'apple'
   const banana = 'banana'
   return `{$apple} {$banana}`
}
```

3. localization safe
```
apple: '{color} color'

appLocalization.getString('apple', {color: 'red'})
```
will show as 'red color'

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
