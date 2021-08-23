<script lang="ts">
  import DataTable, {Head, Body, Row, Cell} from '@smui/data-table'
  import Textfield from '@smui/textfield'
  import Button, { Label} from '@smui/button'
  import Checkbox from '@smui/checkbox'

  let list = [
    {
      itemName: '染色',
      range: '70-120',
      value: '80'
    }
  ]
  let selected = []
  function addItem() {
    list = [...list, {
      itemName: '',
      range: '',
      value: ''
    }]
  }
  function delItem() {
    list = list.filter(el => !selected.includes(el.itemName))
  }
</script>

<div>
  <Button on:click={addItem} variant="outlined">
    <Label>添加检验项</Label>
  </Button>
  <Button on:click={delItem} variant="outlined">
    <Label>删除检验项</Label>
  </Button>
</div>
<DataTable style="max-width:100%;">
  <Head>
    <Row>
      <Cell checkbox><Checkbox /></Cell>
      <Cell>检验项</Cell>
      <Cell>合理值范围</Cell>
      <Cell>测量值</Cell>
    </Row>
  </Head>
  <Body>
    {#each list as item}
    <Row>
      <Cell checkbox>
        <Checkbox bind:group={selected} value={item.itemName}/>
      </Cell>
      <Cell>
        <Textfield bind:value={item.itemName} required/>
      </Cell>
      <Cell>
        <Textfield bind:value={item.range} required/>
      </Cell>
      <Cell>
        <Textfield bind:value={item.value} required/>
      </Cell>
    </Row>
    {/each}
  </Body>
</DataTable>
