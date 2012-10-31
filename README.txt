/* 
 *  Setup:
 *  Create an empty GameObject and add the EventManager script to it.
 *  Create custom event classes that extend the CustomEvent.
 * 
 *  Restrictions & Tips:
 *  DO NOT add event listeners in the Awake() method! 
 *  This is used by the EventManager to initialize.
 * 	Change this class' Execution Order to before default time if you need to work around this.
 *  Use the Start() method to setup your events.
 * 	Make event listener callback functions public.
 *  Extend the CustomEvent class when creating your events.
 * 	Use custom variables in your custom events over the arguments hashtable to maintain class abstraction
 *  Clean up and remove event listeners when objects are destroyed.
 * 	Events are not received if the listener gameObject.active is false.
 * 
 *  Examples:
 * 
 * 	// setup event listeners
 * 	void Start() {
 * 		EventManager.instance.addEventListener(CustomEventObj.EVENT_TO_LISTEN_TO, gameObject, "OnSomethingHappened");
 *  }
 *  
 * 	// remove event listeners
 *  void OnDestroy() {
 *  	if (gameObject) {
 * 			// remove a single event
 * 			EventManager.instance.removeEventListener(CustomEventObj.EVENT_TO_LISTEN_TO, gameObject);
 * 			// remove all events
 * 			EventManager.instance.removeAllEventListeners(gameObject);
 * 		}
 * 	}
 * 
 * 	// get values passed by events
 * 	public void OnSomethingHappened(CustomEventObj evt) {
 * 		Debug.Log((datatype)evt.arguments["value"]);
 * 		// or if using custom vars instead of arguments hashtable
 * 		Debug.Log(evt.rockOn);		
 * 	}
 * 
 * 	// dispatch events
 *  void TriggerEvent() {
 *  	CustomEventObj evt = new CustomEventObj(CustomEventObj.EVENT_TO_TRIGGER);
 *  	evt.arguments.Add("value", 3);
 * 		EventManager.instance.dispatchEvent(evt);
 * 	}
 * 
 *  // create custom events
 *  using UnityEngine;
 *  using System.Collections;
 * 
 *  public class CustomEventObj : CustomEvent {
 * 
 * 		// event types
 *  	public static string MY_EVENT_1 = "my_event_1";
 *  	public static string MY_EVENT_2 = "my_event_2";
 * 
 * 		// optionally add custom variables instead of using the arguments hashtable
 * 		public int myCustomEventVar1 = 0;
 * 		public bool rockOn = true;
 * 
 * 		public CustomEventObj(string eventType = "") {
 *         type = eventType;
 *		}
 *  }
 * 
 */