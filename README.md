# angular2-signaturepad
Angular 2 component for [szimek/signature_pad](https://www.npmjs.com/package/signature_pad).

## Install
`npm install angular2-signaturepad --save`

## Usage example

API is identical to [szimek/signature_pad](https://www.npmjs.com/package/signature_pad).

Options are as per [szimek/signature_pad](https://www.npmjs.com/package/signature_pad) with the following additions:
* canvasWidth: width of the canvas (px)
* canvasHeight: height of the canvas (px)
The above options are provided to avoid accessing the DOM directly from your component to adjust the canvas size.

```typescript
import { Component, ViewChild } from 'angular2/core';
import { SignaturePad } from 'angular2-signaturepad';

@Component({
  template: '<signature-pad [options]="signaturePadOptions" (onEndEvent)="doOnEnd()"></signature-pad>',
  directives: [SignaturePad]
})

export class SignaturePadPage{

  @ViewChild(SignaturePad) signaturePad: SignaturePad;

  private signaturePadOptions: Object = { // passed through to szimek/signature_pad constructor
    'minWidth': 5,
    'canvasWidth': 500,
    'canvasHeight'
  };

  constructor() {
    // no-op
  }

  ngAfterViewInit() {
    // this.signaturePad is now available
    this.signaturePad.set('minWidth', 5); // set szimek/signature_pad options at runtime
    this.signaturePad.clear(); // invoke functions from szimek/signature_pad API
  }

  doOnEnd() {
    // will be notified of szimek/signature_pad's onEnd event
    console.log(this.signaturePad.toDataURL());
  }
}
```
