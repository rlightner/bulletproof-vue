<script setup lang="ts">
import { TrashIcon } from "@heroicons/vue/outline";

import { BaseButton, ConfirmationDialog } from "@/components/Elements";

import { useDeleteComment } from "../api/deleteComment";

type DeleteCommentProps = {
  id: string;
  discussionId: string;
};

const props = defineProps<DeleteCommentProps>();

const { isLoading, isSuccess, mutateAsync } = useDeleteComment({
  discussionId: props.discussionId,
});

async function onClick() {
  await mutateAsync({ commentId: props.id });
}
</script>

<template>
  <ConfirmationDialog
    :isDone="isSuccess"
    icon="danger"
    title="Delete Comment"
    body="Are you sure you want to delete this comment?"
  >
    <template #triggerButton>
      <BaseButton variant="danger" size="sm">
        <template #startIcon>
          <TrashIcon class="h-4 w-4" />
        </template>
        Delete Comment
      </BaseButton>
    </template>
    <template #confirmButton>
      <BaseButton
        @click="onClick"
        :isLoading="isLoading"
        type="button"
        class="bg-red-600"
      >
        Delete Comment
      </BaseButton>
    </template>
  </ConfirmationDialog>
</template>
