/**
* @mainpage
* @section intro Introduction
* Welcome to ActiveTick Feed C++ API.
* 
* This API provides functionality to establish sessions to ActiveTick data feed servers, process requests for static snapshot data, 
* and subscribe to dynamic streaming data feed updates.
*
* This document assumes that the developer is knowledgeable with C and C++, data structures, callback mechanisms, and asynchronous development.
*
* Majority of ActiveTick Feed API consists of standard C-style functions that are used for establishing data feed server connectivity, 
* creating various requests, and sending them to the servers. Additionally, the API provides a number of C++ wrappers that can be used to 
* easily parse responses coming from the servers.
*
* The API is broken down into three categories:
*
* @li Session management
* @li Request/response processing
* @li Dynamic stream updates processing
* 
* Session management API deals with establishing session with the servers, maintaining it, and closing it. Before any type of request can be
* sent to the server, a valid session must be established with the server. To establish a session, the following sequence of API calls must be followed:
*
* @li ATInitAPI()
* @li ATCreateSession()
* @li ATSetAPIUserId()
* @li ATSetStreamUpdateCallback()
* @li ATInitSession()
* @li ATCreateLoginRequest()
* @li ATSendRequest()
* 
* To clean up the API, the following sequence of API calls must be followed:
*
* @li ATShutdownSession()
* @li ATDestroySession()
* @li ATShutdownAPI()
* 
* Once a session is established, the API can submit and process requests for market data.
*
* Request/response processing utilizes asynchronous request-response pattern. All requests initiated by the API do not block, but are returned 
* immediately. During creation of request, the API accepts a callback function used to notify when response is received by API. When server 
* processes requests and API receives responses from the server, a supplied callback is invoked with response data. The callback invocation 
* happens from an internal API thread, and the user of API must be prepared to properly deal with data arriving from a different thread.
*
* All request functions within API are thread-safe and can be called from multiple threads.
*
* To send a request to the server, the request must first be created, and then sent to the server using ATSendRequest() function. The API 
* supports the following requests:
*
* @li ATCreateBarHistoryDbRequest()
* @li ATCreateTickHistoryDbRequest()
* @li ATCreateMarketHolidaysRequest()
* @li ATCreateMarketMoversDbRequest()
* @li ATCreateMarketMoversStreamRequest()
* @li ATCreateQuoteDbRequest()
* @li ATCreateQuoteStreamRequest()
* @li ATCreateSectorListRequest()
* @li ATCreateConstituentListRequest()
* 
* Each request function takes a callback parameter to invoke it once a response is received. If request takes longer time then the allowed time 
* specified during ATSendRequest() call, the supplied ATRequestTimeoutCallback() will be invoked to indicate such event. 
* 
* Dynamic stream updates processing deals with subscription model. Once a symbol or array of symbols is subscribed to using ATCreateQuoteStreamRequest() 
* function, the server starts forwarding updates to the API session. The ATQuoteStreamResponseCallback() is invoked each time an update is received from the server.
* 
* The API keeps a local copy of all subscribed symbols. If disconnect and reconnect happens during live session, the API will automatically re-subscribe 
* all symbols from internal list.
* 
* For development support, the following email can be used to submit development questions related to the API: support@activetick.com
*
* Happy coding!
*/
