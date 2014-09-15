## Emojicon

Whatsapp like implementation for emjoicons which appear as a popup over the  soft keyboard

![Screenshot](/sample.png?raw=true)

## Example


```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              xmlns:emojicon="http://schemas.android.com/apk/res-auto"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:id="@+id/root_view"
              android:orientation="vertical">

    <github.ankushsachdeva.emojicon.EmojiconEditText
            android:id="@+id/editEmojicon"
            android:text="I \ue32d emojicon"
            emojicon:emojiconSize="28sp"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>
</LinearLayout>
```

```java
// Give the topmost view of your activity layout hierarchy. This will be used to measure soft keyboard height
PopupWindow popup = new EmojiconsPopup(rootView, getActivity());

//Will automatically set size according to the soft keyboard size        
popup.setSizeForSoftKeyboard();

//Set on emojicon click listener
popup.setOnEmojiconClickedListener(new OnEmojiconClickedListener() {
            
            @Override
            public void onEmojiconClicked(Emojicon emojicon) {
                emojiconEditText.append(emojicon.getEmoji());
            }
        });

//Set on backspace click listener
popup.setOnEmojiconBackspaceClickedListener(new OnEmojiconBackspaceClickedListener() {
    
    @Override
    public void onEmojiconBackspaceClicked(View v) {
        KeyEvent event = new KeyEvent(
                 0, 0, 0, KeyEvent.KEYCODE_DEL, 0, 0, 0, 0, KeyEvent.KEYCODE_ENDCALL);
                 emojiconEditText.dispatchKeyEvent(event);
    }
});

//Set listener for keyboard open/close
popup.setOnSoftKeyboardOpenCloseListener(new OnSoftKeyboardOpenCloseListener() {
            
            @Override
            public void onKeyboardOpen(int keyBoardHeight) {
                if(!popup.isShowing()){
                    popup.showAtBottom();
                }
            }
            
            @Override
            public void onKeyboardClose() {
                if(popup.isShowing())
                    popup.dismiss();
            }
        });

//To show popup manually you can call popup.showAtBottom();
```

Note: You can change the size of emojis in XML layout through attribute `emojiconSize`.

Note : `EmojiconTextView`: a `TextView` which can render emojis.

Note : `EmojiconEditText`: a `EditText` which can render emojis.


## Acknowledgements

Based on Hieu Rocker's library [Emojicon Github](https://github.com/rockerhieu/emojicon/)

Emojicon is using emojis graphics from [emoji-cheat-sheet.com](https://github.com/arvida/emoji-cheat-sheet.com/tree/master/public/graphics/emojis).

## Contributing

Please fork this repository and contribute back using
[pull requests](https://github.com/rockerhieu/emojicon/pulls).

Any contributions, large or small, major features, bug fixes, additional
language translations, unit/integration tests are welcomed and appreciated
but will be thoroughly reviewed and discussed.

## License

* [Apache Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)

```
Copyright 2014 Ankush Sachdeva

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

 http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
