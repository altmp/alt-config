# alt-config

## Usage:
## config.cpp
```cpp
#include "config.h"

bool Config::Load(const std::wstring& fileName)
{
    std::ifstream ifile(fileName);
    alt::config::Parser parser(ifile);

    try
    {
        node = parser.Parse();

        test = node["test"].ToBool(true);
        test = node["test"].ToString("true");
    }
    catch (const alt::config::Error& e)
    {
        std::cout << e.what() << std::endl;
    }

    return true;
}

bool Config::Save(const std::wstring& fileName)
{
    node["test"] = test;

    std::ofstream ofile(fileName);
    alt::config::Emitter().Emit(node, ofile);

    return true;
}
```
## config.h
```cpp
#include "alt-config.h"

class Config {
public:
	std::string test;
	bool Load(const std::wstring& fileName);
	bool Save(const std::wstring& fileName);
private:
	alt::config::Node node;
};
```
