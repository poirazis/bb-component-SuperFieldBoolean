<script>
  import { getContext, onDestroy } from "svelte";
  import { SuperField, CellBoolean } from "@poirazis/supercomponents-shared";

  const { styleable, builderStore, Provider } = getContext("sdk");
  const component = getContext("component");

  const formContext = getContext("form");
  const formStepContext = getContext("form-step");
  const groupLabelPosition = getContext("field-group");
  const labelWidth = getContext("field-group-label-width");
  const groupColumns = getContext("field-group-columns");
  const groupDisabled = getContext("field-group-disabled");
  const formApi = formContext?.formApi;

  export let field = "Boolean Field";
  export let controlType;
  export let role = "formInput";
  export let labelPosition = "fieldGroup";
  export let template;
  export let helpText;

  export let label;
  export let inlineLabel;
  export let span = 6;

  export let showDirty;

  export let defaultValue;
  export let disabled;
  export let readonly;
  export let validation;
  export let invisible = false;

  export let icon;

  export let onChange;

  let formField;
  let formStep;
  let fieldState;
  let fieldApi;
  let fieldSchema;
  let value;
  let cellState;

  $: formStep = formStepContext ? $formStepContext || 1 : 1;
  $: labelPos =
    groupLabelPosition && labelPosition == "fieldGroup"
      ? groupLabelPosition
      : labelPosition;

  $: formField = formApi?.registerField(
    field,
    "boolean",
    defaultValue,
    disabled,
    readonly,
    validation,
    formStep
  );

  $: unsubscribe = formField?.subscribe((value) => {
    fieldState = value?.fieldState;
    fieldApi = value?.fieldApi;
    fieldSchema = value?.fieldSchema;
  });

  $: value = fieldState?.value ?? defaultValue;
  $: error = fieldState?.error;

  $: cellOptions = {
    defaultValue,
    disabled: disabled || groupDisabled || fieldState?.disabled,
    template,
    readonly: readonly || fieldState?.readonly,
    debounce: formContext ? false : 10,
    icon,
    padding: "0.5rem",
    align: "flex-start",
    role,
    controlType,
    showDirty,
    inlineLabel,
  };

  $: $component.styles = {
    ...$component.styles,
    normal: {
      ...$component.styles.normal,
      display:
        invisible && !$builderStore.inBuilder
          ? "none"
          : $component.styles.normal.display,
      opacity: invisible && $builderStore.inBuilder ? 0.6 : 1,
      "grid-column": groupColumns ? `span ${span}` : "span 1",
      overflow: "hidden",
    },
  };

  const handleChange = (newValue) => {
    value = newValue;
    onChange?.({ value: newValue });
    fieldApi?.setValue(newValue);
  };

  onDestroy(() => {
    fieldApi?.deregister();
    unsubscribe?.();
  });
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-noninteractive-tabindex -->
<div use:styleable={$component.styles}>
  <Provider data={{ value }} />
  <SuperField {labelPos} {labelWidth} {field} {label} {error} {helpText}>
    <CellBoolean
      bind:cellState
      {cellOptions}
      {value}
      {fieldSchema}
      on:change={(e) => handleChange(e.detail)}
    />
  </SuperField>
</div>
