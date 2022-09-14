# di4injector
DI for Injector

## How to use

```shell
pip install di4injector
```

```python
# at example.py

import abc
from di import DIContainer, DI


class GreetingService(abc.ABC):
    @abc.abstractmethod
    def greeting(self) -> str:
        pass

    
class EnglishGreetingService(GreetingService):
    def greeting(self) -> str:
        return 'Hello'


class JapaneseGreetingService(GreetingService):
    def greeting(self) -> str:
        return 'こんにちは'


DIContainer.instance().register(DI.of(
    GreetingService,  # Abstract class 
    {  # inject
        "JP": JapaneseGreetingService,  # ENV=JP  
        "EN": EnglishGreetingService    # ENV=EN
    }, 
    EnglishGreetingService  # Default
))

greeting_service = DIContainer.instance().resolve(GreetingService)
greeting_service.greeting()
```