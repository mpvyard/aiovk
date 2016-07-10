# aiovk
vk.com API python wrapper for asyncio
for old version of python you can use https://github.com/dimka665/vk

### Features
* asynchronous
* support only python 3.5
* have one dependency `aiohttp`
* support two-factor authentication

# Examples
### Annotation
In all the examples below, I will give only the {code}

    async def func():
        {code}

    loop = asyncio.get_event_loop()
    loop.run_until_complete(func())


### Authorisation
**TokenSession** - if you already have token or you use requests which don't require token

    >>> session = TokenSession()
    >>> session = TokenSession(access_token='asdf123..')

**ImplicitSession** - for client authorisation in js apps and standalone (desktop and mobile) apps

    >>> session = ImplicitSession(USER_LOGIN, USER_PASSWORD, APP_ID)
    >>> await session.authorize()
    >>> session.access_token
    asdfa2321afsdf12eadasf123...

With scopes:

    ImplicitSession(USER_LOGIN, USER_PASSWORD, APP_ID, 'notify')
    ImplicitSession(USER_LOGIN, USER_PASSWORD, APP_ID, 'notify,friends')
    ImplicitSession(USER_LOGIN, USER_PASSWORD, APP_ID, ['notify', 'friends'])
    ImplicitSession(USER_LOGIN, USER_PASSWORD, APP_ID, 3)  # notify and friends

Also you can use `SimpleImplicitSession` for entering confirmation code
or captcha key

### VK API
First variant:

    >>> session = TokenSession()
    >>> api = API(session)
    >>> await api.users.get(user_ids=1)
    [{'first_name': 'Pavel', 'last_name': 'Durov', 'id': 1}]

Second variant:

    >>> session = TokenSession()
    >>> api = API(session)
    >>> await api('users.get', user_ids=1)
    [{'first_name': 'Pavel', 'last_name': 'Durov', 'id': 1}]

Also you can add `timeout` argument for each request or define it in the session
