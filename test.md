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
#### Network
```
import { getNetworkStatus, NetworkStatus } from 'axle-react-native-platform/lib/network'
import { jestMockFunction } from 'axle-slac-react-native-platform/lib/utils/test-utils'
 
jest.mock('axle-react-native-platform/lib/network', () => {
    return {
        getNetworkStatus: jest.fn()
    }
})
 
describe('SleepEditSessionSaveButton', () => {
    it('should return network error message there is no internet and app is foreground', async done => {
        jestMockFunction(getNetworkStatus).mockImplementation(async () => {
            return <NetworkStatus>{
                type: {
                    name: 'WiFi'
                },
                isInternetReachable: false
            }
        })
        AppState.currentState = 'active'
        const saveResult = await saveEditableSleepSessionResult('save', RELATIVE_TIME_TODAY, START_TIME, END_TIME)
        expect(saveResult).toStrictEqual({
            type: 'networkError',
            editType: 'save'
        })
        done()
    })
})
 ```

#### onPress

```
describe(`SleepLandingFallbackHeroCardLeftContent`, () => {
    it(`should properly invoke externally provided callback on press`, () => {
        const ON_PRESS_CALLBACK = jest.fn()
        const TIME_ASLEEP_FEATURE:FeatureAwareAttribute<number | null > = {
            featureStatus:'Available',
            value: 123
        }
 
 
        const { getByTestId } = render(<SleepLandingFallbackHeroCardLeftContent
        granularity='D'
        onPressHeroTimeAsleep={ON_PRESS_CALLBACK}
        title={USED_TITLE}
        timeAsleepFeature={TIME_ASLEEP_FEATURE}
 
        />)
 
        fireEvent.press(getByTestId(SleepLandingFallbackHeroCardLeftContent.TestIds.heroScoreDisplay))
        expect(ON_PRESS_CALLBACK).toHaveBeenCalled()
    })
})
```

#### Navigation

```
// Mock navigate()
jest.mock('axle-react-native-navigation', () => {
    return {
        navigate: jest.fn()
    }
})
 
// Define expected navigation destination page
const EXPECTED_NAVIGATION_PARAMS: Parameters<typeof navigate>[0] = 'ActivityPage'
const MOCKED_DATE = new Date(2021, 10, 9)
 
describe(`ActivityHomeFeedGoalCard`, () => {
    beforeAll(() => {
        Settings.now = () => MOCKED_DATE.valueOf()
    })
    afterAll(() => {
        Settings.resetCaches()
    })
    it('should navigate to current weekly ActivityPage', () => {
        const { getByTestId } = render(
            <ActivityHomeFeedGoalCard
                type={'goal'}
                weekScore={WEEK_SCORE_TEST}
                goalRecord={ACTIVITY_GOAL_RECORD_TEST}
            />
        )
        fireEvent.press(getByTestId(ActivityHomeFeedGoalCard.TestIds.feedCard))
        expect(navigate).toBeCalledWith(EXPECTED_NAVIGATION_PARAMS, {
            initialTimeWindow: {
                referenceTime: MOCKED_DATE,
                timeGranularity: 'W'
            }
        })
    })
})

```
#### Navigation with onPress

```
// Mock navigate()
jest.mock('axle-react-native-navigation', () => {
    return {
        navigate: jest.fn()
    }
})
 
// Define expected navigation destination page
const EXPECTED_NAVIGATION_PARAMS: Parameters<typeof navigate>[0] = 'ActivityPage'
const MOCKED_DATE = new Date(2021, 10, 9)
 
describe(`ActivityHomeFeedGoalCard`, () => {
    beforeAll(() => {
        Settings.now = () => MOCKED_DATE.valueOf()
    })
    afterAll(() => {
        Settings.resetCaches()
    })
    it('should navigate to current weekly ActivityPage', () => {
        const { getByTestId } = render(
            <ActivityHomeFeedGoalCard
                type={'goal'}
                weekScore={WEEK_SCORE_TEST}
                goalRecord={ACTIVITY_GOAL_RECORD_TEST}
            />
        )
        fireEvent.press(getByTestId(ActivityHomeFeedGoalCard.TestIds.feedCard))
        expect(navigate).toBeCalledWith(EXPECTED_NAVIGATION_PARAMS, {
            initialTimeWindow: {
                referenceTime: MOCKED_DATE,
                timeGranularity: 'W'
            }
        })
    })
})
```


####  getByTestId & getByType
    Use `getByTestId` for when a component exists
    Use `queryByTestId` for when a component is null
 
```
it(`should show non-member view when feature is not available`, () => {
    ;(useDebugSleepSchemaMembershipOverrides as jest.Mock).mockImplementation(() => {
        const SLEEP_SUMMARY_SCHEMA: SleepSummarySchemaDayData = {
            ...SleepSummarySchemaTestUtils.dayZeroSchemaData,
            historicalMembershipStatus: 'Unavailable'
        }
        return SLEEP_SUMMARY_SCHEMA
    })
    ;(useCurrentMembershipStatus as jest.Mock).mockImplementation(() => {
        const featureStatus: FeatureStatus = 'Unavailable'
        return featureStatus
    })
    const { getByTestId, queryByTestId } = render(
        <SleepDomainHubCarouselCard testID={UNUSED_TEST_ID} type="carousel-card" />
    )
    expect(getByTestId(SleepDomainHubCarouselCard.TestIds.nonMemberContent)).toBeDefined()
    expect(queryByTestId(SleepDomainHubCarouselCard.TestIds.memberContent)).toBeNull()
})



it(`should show if valid intervals, relativeTime is today, and useShouldShowEditableSleep is true`, () => {
    ;(useShouldShowEditableSleep as jest.Mock).mockReturnValue(true)
 
    const { getByType } = render(
        <EditableSleepRow
            historicalMembershipStatus="Available"
            intervals={VALID_INTERVALS}
            isSimplifiedSleepSession={false}
            relativeTime={RELATIVE_TIME_TODAY}
            sleepArchitecture={null}
            onDomainPageSleepProcessingChanged={() => {}}
            editSummaryType={EditSummaryType.NotEdited}
        />
    )
 
    expect(getByType(View)).toBeDefined()
})
```

#### Promise

```
const SAVE_ON_SHOW_NETWORK_ERROR_CALLBACK = jest.fn()
const SAVE_ON_SHOW_SERVER_ERROR_CALLBACK = jest.fn()
const SAVE_ON_SAVE_SUCCESS_CALLBACK = jest.fn()
const SAVE_ON_SHOW_LOADING_CALLBACK = jest.fn()
const SAVE_ON_STOP_LOADING_CALLBACK = jest.fn()
 
it('should use server error callback when it returns server error message for saving', async done => {
        jestMockFunction(saveEditableSleepSessionResult).mockResolvedValue({
            type: 'serverError',
            editType: 'save'
        })
 
        const saveProps = createSaveProps()
        await sendSaveSleepEditSession(
            'save',
            saveProps.sleepEditSessionSaveErrorPageController.onShowSaveNetworkErrorPage,
            saveProps.sleepEditSessionSaveErrorPageController.onShowSaveServerErrorPage,
            saveProps.onEditSessionLoadingProcessing,
            saveProps.onEditSessionLoadingCompleted,
            saveProps.relativeTimeDay,
            saveProps.startTime,
            saveProps.endTime,
            saveProps.onSleepSessionSaved,
            saveProps.onSleepSessionNotSaved,
            saveProps.workflowInstanceId,
            saveProps.dismissModal
        )
 
        expect(saveEditableSleepSessionResult).toHaveBeenCalled()
        expect(SAVE_ON_SHOW_LOADING_CALLBACK).toHaveBeenCalled()
        expect(SAVE_ON_STOP_LOADING_CALLBACK).toHaveBeenCalled()
        expect(SAVE_ON_SHOW_NETWORK_ERROR_CALLBACK).not.toHaveBeenCalled()
        expect(SAVE_ON_SHOW_SERVER_ERROR_CALLBACK).toHaveBeenCalled()
        expect(SAVE_ON_SAVE_SUCCESS_CALLBACK).not.toHaveBeenCalled()
        done()
})
```

#### Date

```
const MILLIS = DateTime.fromObject({ year: 2021, month: 6, day: 16 }).valueOf()
 
describe('<SettingsMain />', () => {
    beforeAll(() => {
        Settings.now = () => MILLIS
    })
 
    afterAll(() => {
        Settings.resetCaches()
    })
})
```

#### FakeTimers

```
//========================================
// DON'T DO THIS
//========================================
// describe(`testing timeout`, () => {
//     it('waits 1000 real milliseconds seconds', async () => {
//         await new Promise(resolve => setTimeout(resolve, 1_000))
//     })
// })
 
//========================================
// DO THIS
//========================================
jest.useFakeTimers()
 
describe(`testing timeout`, () => {
    it('simulates waiting 1000 milliseconds but complete almost synchronously', async () => {
        const promise = new Promise(resolve => setTimeout(resolve, 1_000))
        jest.advanceTimersByTime(1_000)
        await promise
    })
})
```


