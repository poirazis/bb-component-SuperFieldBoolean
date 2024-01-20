<script>
  import { getContext , onDestroy} from "svelte";
  import CellBoolean from "../../bb_super_components_shared/src/lib/SuperCell/cells/CellBoolean.svelte";

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  const formContext = getContext("form");
  const formStepContext = getContext("form-step");
  const labelPos = getContext("field-group");
  const labelWidth = getContext("field-group-label-width");
  const formApi = formContext?.formApi;

  export let field;
  export let controlType
  export let template

  export let label;
  export let span = 6;

  export let defaultValue
  export let disabled
  export let readonly
  export let validation

  export let icon

  export let onChange

  let formField;
  let formStep;
  let fieldState;
  let fieldApi;
  let fieldSchema
  let value;
  let cellState
  

  $: formStep = formStepContext ? $formStepContext || 1 : 1;

  $: formField = formApi?.registerField(
    field,
    "boolean",
    defaultValue,
    disabled,
    readonly,
    validation,
    formStep
  )

  $: unsubscribe = formField?.subscribe((value) => {
    fieldState = value?.fieldState;
    fieldApi = value?.fieldApi;
    fieldSchema = value?.fieldSchema;
  });

  $: value = fieldState?.value

  $: cellOptions = { 
      defaultValue,
      disabled,
      template,
      readonly: readonly || disabled,
      icon,
      align: "flex-start",
      role: "formInput", 
    }


  $: $component.styles = {
    ...$component.styles,
    normal: {
      ...$component.styles.normal,
      "flex-direction": labelPos == "left" ? "row" : "column",
      gap: labelPos == "left" ? "0.85rem" : "0rem",
      "grid-column": labelPos ? "span " + span : null,
      "--label-width":
        labelPos == "left" ? (labelWidth ? labelWidth : "6rem") : "auto",
    },
  };
  
  const handleChange = ( newValue ) => {
    console.log("Setting Value ", newValue)


    onChange?.({value: newValue});
    fieldApi?.setValue(newValue);
  }

  onDestroy(() => {
    fieldApi?.deregister()
    unsubscribe?.()
  })
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-noninteractive-tabindex -->
<div
  class="superField"
  on:focus={cellState.focus} 
  tabindex="0"
  use:styleable={$component.styles}  
>
  <label for="superCell" class="superlabel" class:bound={formContext}>
    {label}
  </label>
  
  <div class="inline-cells">
    <CellBoolean
      bind:cellState
      {cellOptions}
      {value}
      {fieldSchema}
      on:change={(e) => handleChange(e.detail)}
      on:blur={cellState.lostFocus}
    />
  </div>
</div>

<style>
  .superField {
    display: flex;
    align-items: stretch;
    justify-content: stretch;
    min-width: 0;
  }

  .superField:focus {
    outline: none;
  }
  .superlabel {
    display: flex;
    align-items: flex-start;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    min-width: var(--label-width);
    max-width: var(--label-width);
    font-size: 12px;
    line-height: 1.75rem;
    font-weight: 400;
    color: var(--spectrum-global-color-gray-700);
  }

  .inline-cells {
    flex: 1;
    display: flex;
    justify-items: stretch;
    height: 2rem;
  }

  .superlabel.bound {
    gap: 0.5rem;
  }
</style>



