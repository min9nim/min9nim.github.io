---
layout: post
title:  "[vue-composition-api] computed 사용시 주의할 점"
date:   2019-08-27 00:10
categories: vue
tags: [vue, commposition]
---
아래와 같이 `caseInfo` 프롭을 가져와서 사용하면 `computed` 속성 `eventProps` 가 reactive 하지 않다(변경되는 prop값에 따라 반응하지 않는다)

```javascript
import {computed, createComponent, reactive} from '@vue/composition-api'
import {pick} from '~/utils'
import AtatchFiles from './atatch-files/index.vue'

export default createComponent({
  components: {
    AtatchFiles,
  },
  props: {
    caseId: String,
    caseInfo: Object,
    item: Object,
  },
  setup({caseInfo}){
    const state = reactive({
      courtEventList: ['전체', '법원 기일', '법원 명령', '법원문서 발송', '법원문서 제출'],
      courtEventFilter: 0,
      eventProps: computed(() => {
        const props = pick(['dateProp', 'cmdProp', 'docProp', 'transferProp'])(caseInfo)
        return Object.entries(props)
      }),
      caseBasicInfoView: true,
      caseInvolvedInfoView: true,
      caseRelatedInfoView: true,
      caseEventInfoView: true,
      caseFileInfoView: true,
      caseDocumentInfoView: true,
    })
    return {
      state,
    }
  },
})
```
아래와 같이 `computed` 함수에서 `initProps` 를 직접 접근해야하면 reactive 해진다

```javascript
import {computed, createComponent, reactive} from '@vue/composition-api'
import {pick} from '~/utils'
import AtatchFiles from './atatch-files/index.vue'

export default createComponent({
  components: {
    AtatchFiles,
  },
  props: {
    caseId: String,
    caseInfo: Object,
    item: Object,
  },
  setup(initProps){
    const state = reactive({
      courtEventList: ['전체', '법원 기일', '법원 명령', '법원문서 발송', '법원문서 제출'],
      courtEventFilter: 0,
      eventProps: computed(() => {
        const props = pick(['dateProp', 'cmdProp', 'docProp', 'transferProp'])(initProps.caseInfo)
        return Object.entries(props)
      }),
      caseBasicInfoView: true,
      caseInvolvedInfoView: true,
      caseRelatedInfoView: true,
      caseEventInfoView: true,
      caseFileInfoView: true,
      caseDocumentInfoView: true,
    })
    return {
      state,
    }
  },
})
```

이유는 뭐 잘 모르겠다. call-by-value, call-by-reference 뭐 그런거 겠지