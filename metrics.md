```
/**
 * Sleep edit page workflow event.
 */
interface EditableSleepWorkflow extends Event {
    name: 'WORKFLOW'
    attributes: {
        eventId: 'editable_sleep_workflow'
        pageId: pageIdType
        domainName: 'sleep'
        workflowName: 'sleep_edit'
        workflowInstanceId: string
        workflowIdType: 'system'
        action: editableSleepWorkflowActionType
    }
    metrics: {}
}

/**
 * Events from interactions with sleep edit page.
 */
interface SleepDomainPencilInteraction extends Event {
    name: 'INTERACTION'
    attributes: {
        eventId: 'sleep_domain_page_editable_sleep_row_interaction'
        pageId: pageIdType
        domainName: 'sleep'
        action: 'tap'
        objectType: 'button'
        objectName: 'start_sleep_edit_session'
    }
    metrics: {}
}

type EditableSleepInteractionEvents = SleepDomainPencilInteraction |  EditableSleepWorkflow

/**
 * Event Logger
 */
const editableSleepLogEvent = createEventLogger<EditableSleepInteractionEvents>()

export const editableSleepLogEvents = {
    logEditableSleepWorkflowEvent: (workflowInstanceId: string, action: editableSleepWorkflowActionType) => {
        editableSleepLogEvent({
            name: 'WORKFLOW',
            attributes: {
                eventId: 'editable_sleep_workflow',
                pageId: sleepLandingPageId,
                domainName: 'sleep',
                workflowName: 'sleep_edit',
                workflowInstanceId: workflowInstanceId,
                workflowIdType: 'system',
                action: action
            },
            metrics: {}
        })
    },
    logSleepDomainPencilInteractionEvent: () => {
        editableSleepLogEvent({
            name: 'INTERACTION',
            attributes: {
                eventId: 'sleep_domain_page_editable_sleep_row_interaction',
                pageId: sleepLandingPageId,
                domainName: 'sleep',
                action: 'tap',
                objectType: 'button',
                objectName: 'start_sleep_edit_session'
            },
            metrics: {}
        })
    }
  }
```
