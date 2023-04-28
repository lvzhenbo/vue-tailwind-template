<template>
  <!-- Tailwindcss Intellisense can run here -->
  <div class="w-full">
    <n-data-table
    :columns="columns"
    :data="data"
    :pagination="pagination"
    :bordered="false"
  />
  </div>
</template>

<script lang="tsx">
import { defineComponent } from 'vue'
import { NButton, NDataTable } from 'naive-ui'
import type { DataTableColumns } from 'naive-ui'

type Song = {
  no: number
  title: string
  length: string
}

const createColumns = ({
  play
}: {
  play: (row: Song) => void
}): DataTableColumns<Song> => {
  return [
    {
      title: 'No',
      key: 'no'
    },
    {
      title: 'Title',
      key: 'title'
    },
    {
      title: 'Length',
      key: 'length'
    },
    {
      title: 'Action',
      key: 'actions',
      render (row) {
        return (
          // Tailwindcss Intellisense cannot run here
          <div class='flex flex-col'>
            <NButton strong tertiary size='small' onClick={() => play(row)}>Play</NButton>
            <NButton strong tertiary size='small' onClick={() => play(row)}>Play</NButton>
          </div>
        )
      }
    }
  ]
}

const data: Song[] = [
  { no: 3, title: 'Wonderwall', length: '4:18' },
  { no: 4, title: "Don't Look Back in Anger", length: '4:48' },
  { no: 12, title: 'Champagne Supernova', length: '7:27' }
]

export default defineComponent({
  components: {NDataTable},
  setup () {
    return {
      data,
      columns: createColumns({
        play (row: Song) {
          console.log(`Play ${row.title}`)
        }
      }),
      pagination: false as const
    }
  }
})
</script>
