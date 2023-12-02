# How to `clang-format` on Build in Xcode

1. Install clang-format:
    
    ```sh
    $ brew install clang-format
    ```
    
2. Place `.clang-format` file under your project.
3. In Xcode, open `Product` > `Scheme` > `Edit Scheme...` > `Build` > `Pre-actions`.
4. Click `+` button and select your target (`Provide build settings from`).
5. Copy and paste this shell script:

   5-A. If you are using git (**recomended**):
   ```sh
   cd $SRCROOT && git status --porcelain \
   | awk '$1 ~ /^[MA]/ && $2 ~ /\.(cpp|hpp)$/ {print $2}' \
   | xargs /opt/homebrew/bin/clang-format -i -style=file
   ```
   Now your project files ends with `.cpp` or `.hpp` where git status is "added" or "modified" will be formatted on build.


   5-B. Otherwise:
    ```sh
    find -E ${PROJECT_DIR} -regex ".*\.(cpp|hpp)" | xargs /opt/homebrew/bin/clang-format -i -style=file
    ```
    Now your project files ends with `.cpp` or `.hpp` will be formatted on build.
