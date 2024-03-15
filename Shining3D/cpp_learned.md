# CPP_learned
## Day1
### 1. how to open a file on windows
- use system command to open a file with the default application
    ```cpp
    #include <string>
    #include <iostream>
    #include <cstdlib>
    int main() {
        std::string workpath = "D:/test1/bin";
        std::string filename = "DefaultProject.SNIProj";
        std::string command = "start \"\" \"" + workpath + "\\" + filename + "\"";

        // Use the system command to open the file with the default application
        system(command.c_str());

        return 0;
    }
    ```

### 2. Whats Callback function
### 3. 