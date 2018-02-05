Typescript definitions for the old Ext JS 3.4.0 library, if anyone is ever crazy enough to want to use it with TypeScript.

## How to use

Install typings:

	npm i https://github.com/emptyother/types-extjs3/ --save-dev

Example creating a new class from Ext components:

	export class MyWindow extends Ext.Window {
		private textfield = new Ext.form.TextField({
			fieldLabel: 'My text field',
			listeners: {
				keyup: (cmp: Ext.form.TextField, e: Ext.EventObject) => {}
			}
		});
		constructor(cfg: Ext.IPanel = {}) {
			// TS insist that super should be called before everything else
			// so you can't use "this" references inside it.
			super({
				title: 'My title',
				layout: 'form',
				...cfg,
			});
			// TS compiler inserts property initializers here:
			// this.textfield = ...

			// So now we can add our children.
			this.add([
				this.textfield,
			]);
		}
		protected initComponent() {
			// Warning:
			// The super() in the constructor calls initComponent before
			// this.textfield has been initialized, so we can't do stuff here.
		}
	}

## TODO

There is a lot missing, as i added definitions as i needed them.

* Add event listener definitions.
* Rename configuration interface definitions from (using the IPanel as an example) `Ext.IPanel` to `Ext.PanelCfg`.