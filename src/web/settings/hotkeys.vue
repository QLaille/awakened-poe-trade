<template>
  <div class="max-w-md p-2">
    <div class="bg-gray-700 rounded px-2 py-1 mb-2 leading-none">
      <i class="fas fa-info-circle"></i> {{ $t('You can clear hotkey by pressing Backspace') }}</div>
    <div class="mb-8">
      <div class="flex">
        <div class="flex-1">{{ $t('Price check') }}</div>
        <div class="flex">
          <span class="text-gray-500 mr-2">{{ $t('Auto-hide Mode') }}</span>
          <button :class="{ border: config.priceCheckKeyHold === 'Ctrl', 'line-through': config.priceCheckKey === null }" @click="config.priceCheckKeyHold = 'Ctrl'; config.priceCheckKey = null" class="rounded px-1 bg-gray-900 leading-none mr-1">Ctrl</button>
          <button :class="{ border: config.priceCheckKeyHold === 'Alt', 'line-through': config.priceCheckKey === null }" @click="config.priceCheckKeyHold = 'Alt'; config.priceCheckKey = null" class="rounded px-1 bg-gray-900 leading-none">Alt</button>
          <span class="mx-4">+</span>
          <hotkey-input v-model="config.priceCheckKey" :forbidden="['Ctrl','Shift','Alt', ...(config.priceCheckKeyHold === 'Ctrl' ? ['C','V','A','F','Enter'] : [])]" class="w-20" />
        </div>
      </div>
      <div class="text-right mt-2">
        <span class="text-gray-500 mr-2">{{ $t('Open without auto-hide') }}</span>
        <hotkey-input v-model="config.priceCheckLocked" class="w-48" />
      </div>
    </div>
    <div class="mb-4">
      <div class="flex">
        <div class="flex-1">{{ $t('Overlay') }} <span class="text-red-500 text-lg leading-none">*</span></div>
        <hotkey-input required v-model="config.overlayKey" class="w-48" />
      </div>
    </div>
    <div class="mb-4">
      <div class="flex">
        <div class="flex-1">{{ $t('Open item on wiki') }}</div>
        <hotkey-input v-model="config.wikiKey" class="w-48" />
      </div>
    </div>
    <div class="mb-4">
      <div class="flex">
        <div class="flex-1">{{ $t('Map check') }}</div>
        <hotkey-input v-model="config.mapCheckKey" class="w-48" />
      </div>
    </div>
    <div class="mb-8">
      <div class="flex">
        <div class="flex-1">{{ $t('Delve grid') }}</div>
        <hotkey-input v-model="config.delveGridKey" class="w-48" />
      </div>
    </div>
    <div class="mb-8">
      <div class="flex">
        <div class="flex-1">{{ $t('Stash tab scrolling') }}</div>
        <div class="flex">
          <ui-radio v-model="config.stashScroll" :value="true" class="mr-4 font-fontin-regular">Ctrl + MouseWheel</ui-radio>
          <ui-radio v-model="config.stashScroll" :value="false">{{ $t('Disabled') }}</ui-radio>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HotkeyInput from './HotkeyInput'
import { Config } from '@/web/Config'

export default {
  components: { HotkeyInput },
  computed: {
    config () {
      return Config.store
    }
  }
}
</script>

<i18n>
{
  "ru": {
    "You can clear hotkey by pressing Backspace": "Вы можете отключить сочетание, нажав клавишу Backspace",
    "Price check": "Прайс-чек",
    "Auto-hide Mode": "Режим авто-скрытия",
    "Open without auto-hide": "Открыть без авто-скрытия",
    "Overlay": "Оверлей",
    "Open item on wiki": "Открыть предмет в вики",
    "Map check": "Проверка карты",
    "Stash tab scrolling": "Прокрутка вкладок тайника",
    "Delve grid": "Сетка \"Спуска\""
  }
}
</i18n>
