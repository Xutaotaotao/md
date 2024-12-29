<script setup lang="ts">
import { defineEmits, ref } from 'vue'

const emits = defineEmits([`update:isOpen`, `submit`])

const displayStore = useDisplayStore()

const formGitHub = ref({
  repo: ``,
  token: ``,
})

function handleSubmit() {
  if (!formGitHub.value.repo) {
    return
  }
  emits(`submit`, formGitHub.value)
  emits(`update:isOpen`, false)
}
</script>

<template>
  <Dialog v-model:open="displayStore.isShowYuqueFormDialog">
    <DialogContent class="max-w-150">
      <DialogHeader>
        <DialogTitle>语雀 MD 图片转换为 Github 图床图片 </DialogTitle>
      </DialogHeader>
      <div class="space-y-4">
        <FormItem label="GitHub 仓库" required>
          <Input v-model.trim="formGitHub.repo" placeholder="如：yanglbme/resource" />
        </FormItem>
        <FormItem label="Token" required>
          <Input
            v-model.trim="formGitHub.token" type="password"
            placeholder="如：cc1d0c1426d0fd0902bd2d7184b14da61b8abc46"
          />
        </FormItem>
        <FormItem>
          <Button
            variant="link" class="p-0" as="a"
            href="https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token"
            target="_blank"
          >
            如何获取 GitHub Token？
          </Button>
        </FormItem>
      </div>

      <DialogFooter>
        <Button @click="handleSubmit">
          提交
        </Button>
      </DialogFooter>
    </DialogContent>
  </Dialog>
</template>
