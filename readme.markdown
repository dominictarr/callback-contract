#The Callback Contract

"asyncronous" means after the function returns.
"syncronous" means befor the function returns.

## the standard callback contract SCC

  * an asyncronous function MUST take a callback as the last argument.
  when processing is complete, the asyncronous function MUST callback the caller
  via the callback.

  * if an error occured, the first callback argument MUST be the error.

  * if no error occured, the first argument MUST be falsey. (null, undefined, 0, false, '')

  * the asyncronous function MUST NOT callback the caller more than one time. 
  (this is not usually specified explicitly, however, it is necessary for sane control flow)

  * the asyncronous function may throw an exception syncronously. for example, if no callback was provided.
  
  * the asyncronous function MUST NOT throw any exception after the function has returned, 
  that is to say the asyncronous function MUST NOT throw an asyncronous error. 
  Any asyncronous error must be passed back to the caller via the callback.
  
  * the asyncronous function MAY callback syncronously. 
  that is to say, it may callback before the function has returned.
  
  * in the case of a syncronous callback, 
  any error thrown syncronously by the callback should not be caught.

## the ALWAYS asyncronous callback.

the same as _The Standard Contract_, except the callback MUST NOT be called syncronously, 
that is to say before the function returns.

this simplifies handling the case where the callback throws syncronously.
  
## the no throw asyncronous callback, 

this is a strengthening of the always asycnronous callback, 
which demands that there is no syncronous throw. all errors must be passed to the callback.

## the async-if-thruthy contract.

  it advised to be very explicit if using supporting contract. this is not widely supported by node.
  
  -- if return thruthy, no callback.
  -- what if it callsback syncronously?
