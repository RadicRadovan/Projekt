<template>
  <div class="select">
      <select id='cities' @change="onChange($event)">
          <option value="Maribor">Maribor</option>
          <option value="Ljubljana">Ljubljana</option>
          <option vlaue='Celje'>Celje</option>
      </select>
  </div>
</template>

<script>
export default {
    name: 'Selector',
    methods:{
    onChange:function(event){
        this.$emit('mesto',event.target.value);
        }
    }
}
</script>

<style>
:root {
    --select-border: #777;
    --select-focus: #FFBE00;
    --select-arrow: var(--select-border);
}

*,
*::before,
*::after {
    box-sizing: border-box;
}

select {
    appearance: none;
    background-color: transparent;
    border: none;
    padding: 0 1em 0 0;
    margin: 0;
    width: 100%;
    font-family: inherit;
    font-size: inherit;
    cursor: inherit;
    line-height: inherit;
    outline: none;
}



select::-ms-expand {
    display: none;
}

.select {
    width: 100%;
    min-width: 15ch;
    max-width: 30ch;
    border: 1px solid var(--select-border);
    border-radius: 0.25em;
    padding: 0.25em 0.5em;
    font-size: 1.25rem;
    cursor: pointer;
    line-height: 1.1;
    background-color: #fff;
    background-image: linear-gradient(to top, #f9f9f9, #fff 33%);
    display: grid;
    grid-template-areas: "select";
    align-items: center;
    position: relative;
}

select,
.select::after {
    grid-area: select;
}

.select::after {
    content: "";
    width: 0.8em;
    height: 0.5em;
    background-color: var(--select-arrow);
    clip-path: polygon(100% 0%, 0 0%, 50% 100%);
    justify-self: end;
}

select:focus + .focus {
    position: absolute;
    top: -1px;
    left: -1px;
    right: -1px;
    bottom: -1px;
    border: 2px solid var(--select-focus);
    border-radius: inherit;
}

</style>