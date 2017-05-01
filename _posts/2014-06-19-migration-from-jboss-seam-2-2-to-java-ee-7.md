---
id: 420
title: Migration from JBoss Seam 2.2 to Java EE 7
date: 2014-06-19T17:20:48+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=420
permalink: /2014/06/migration-from-jboss-seam-2-2-to-java-ee-7/
categories:
  - Dicas
---
This article is about a migration of application seam-booking from JBoss Seam to Java EE 7, removing JBoss Seam dependency. 

This is important because there lots of legacy JBoss Seam application that must run in newest containers, like Wildfly 8.

<a href="http://www.seamframework.org/Seam2/Downloads" target="_blank">Seam-booking is an example application from JBoss Seam 2 distribution</a>. It uses the following technologies:

* JBoss Seam 2.2
  
* Java Server Faces 1.2
  
* JPA 1.0
  
* Hibernate 3.3.2.GA
  
* Richfaces 3.3.1
  
* Hibernate Validator

The migration is to remove JBoss Seam dependency, update it to Java EE 7, to the following technologies, present in <a href="http://wildfly.org" target="_blank">Wildfly 8.1</a>

* CDI 1.1
  
* JPA 2.1
  
* JSF 2.1
  
* Hibernate 4.3
  
* Richfaces 4.3.5
  
* Picketlink 2.5.2
  
* Bean Validation

Some general notes about the migrated application:

booking is the name I will refer, when talking about the application, seam-booking is the original application.

There were some decisions I did, for example remove EJB and let only CDI Beans, but this move would change too much, and the intent of this article is not to change the architecture of this application, but only change the technologies.

The automated tests were removed from booking, as I am not interested to migrate it.

As a side note, a lighter migration is possible, make the seam-booking works with minimal change, running with JBoss Seam 2.2, hibernate 3.3.2, etc. But that is a subject for other article.

There are many references to the word &#8220;seam&#8221; (package names, explication texts, etc.), I didn&#8217;t remove it because I didn&#8217;t want to change too much of the application, to facilitate the diff operation and to focus in the technology side.

Picketlink is used as the security authenticator, as it integrates with CDI.

## Differences

The differences will be outlined as &#8220;before&#8221; and &#8220;after&#8221; when applicable, the code &#8220;before&#8221; is contained in a box with white background, the &#8220;after&#8221; code is contained in a grey background to facilitate the reading process. Also I will provide some justification why I have implemented that way.

The original seam-booking and booking are available for download, if you want to run a diff and navigate yourself into it.

This is a list of the overall changes, easier to understand, that any migration from JBoss Seam to Java EE 7 must perform.

Also, some EJB interfaces return method names changed, as it uses the JSF 2 implicit navigation to return the page names for each action.

<table width="100%" cellspacing="0" cellpadding="4">
  <colgroup> <col width="50%" /> <col width="50%" /> </colgroup> <tr valign="top">
    <td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0.1cm 0cm 0.1cm 0.1cm;" bgcolor="#eeeeee" width="48%">
      <p align="center">
        <b>JBoss Seam</b>
      </p>
    </td>
    
    <td style="border: 1px solid #000000; padding: 0.1cm;" bgcolor="#eeeeee" width="52%">
      <p align="center">
        <b>Java EE 7</b>
      </p>
    </td>
  </tr>
  
  <tr>
    <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
      <span style="font-family: Courier New,monospace;">@In</span><br /> <span style="font-family: Courier New,monospace;">@Name</span></p> 
      
      <p>
        <span style="font-family: Courier New,monospace;">@Scope(ScopeType.SESSION)</span></td> 
        
        <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
          <span style="font-family: Courier New,monospace;">@Inject</span><span style="font-family: Courier New,monospace;">@Named</span></p> 
          
          <p>
            <span style="font-family: Courier New,monospace;">@SessioScoped</span></td> </tr> 
            
            <tr>
              <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                Only preserves the value if is appropriate. The @Named is only necessary if the bean is used in facelets pages, the #{my_name} instruction. As CDI uses injection by class type,<br /> all classes are eligible to injection between classes of the same deployable artifact.</p> 
                
                <p>
                  &nbsp;</td> </tr> 
                  
                  <tr>
                    <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                      <span style="font-family: Courier New,monospace;">Hibernate validator</span><span style="font-family: Courier New,monospace;">@NotNull</span></p> 
                      
                      <p>
                        <span style="font-family: Courier New,monospace;">@Pattern</span>
                      </p>
                      
                      <p>
                        <span style="font-family: Courier New,monospace;">@Length</span></td> 
                        
                        <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                          <span style="font-family: Courier New,monospace;">Bean validation</span><span style="font-family: Courier New,monospace;">@NotNull</span></p> 
                          
                          <p>
                            <span style="font-family: Courier New,monospace;">@Pattern</span>
                          </p>
                          
                          <p>
                            <span style="font-family: Courier New,monospace;">@Size</span></td> </tr> 
                            
                            <tr>
                              <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                They are minor modifications and easy to understand.</p> 
                                
                                <p>
                                  &nbsp;</td> </tr> 
                                  
                                  <tr>
                                    <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                      <span style="font-family: Courier New,monospace;">@Logger</span>
                                    </td>
                                    
                                    <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                      <span style="font-family: Courier New,monospace;">JUL Logger</span>
                                    </td>
                                  </tr>
                                  
                                  <tr>
                                    <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                      Uses the JUL Logger class, very simple to use.</p> 
                                      
                                      <p>
                                        &nbsp;</td> </tr> 
                                        
                                        <tr>
                                          <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                            <span style="font-family: Courier New,monospace;">@Restrict</span>
                                          </td>
                                          
                                          <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                          </td>
                                        </tr>
                                        
                                        <tr>
                                          <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                            No replacement in Java EE 7. As it only checks for user authentication, I added a servlet filter (SecurityFilter) to check user authentication.</p> 
                                            
                                            <p>
                                              &nbsp;</td> </tr> 
                                              
                                              <tr>
                                                <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                  <span style="font-family: Courier New,monospace;">pages.xml</span>
                                                </td>
                                                
                                                <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                </td>
                                              </tr>
                                              
                                              <tr>
                                                <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                                  seam-booking uses pages.xml to handle navigation, but booking uses JSF implicit navigation and a servlet filter to redirect user if he try to access a protected page.</p> 
                                                  
                                                  <p>
                                                    &nbsp;</td> </tr> 
                                                    
                                                    <tr>
                                                      <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                        <span style="font-family: Courier New,monospace;">@PersistentContext</span>
                                                      </td>
                                                      
                                                      <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                        <span style="font-family: Courier New,monospace;">@Inject</span>
                                                      </td>
                                                    </tr>
                                                    
                                                    <tr>
                                                      <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                                        The entity manager is produced in Resources class, it injects a @PersistenceUnit (EntityManagerFactory) and fabricates a entity manager at the time of the first request, and closes it when disposing.</p> 
                                                        
                                                        <p>
                                                          &nbsp;</td> </tr> 
                                                          
                                                          <tr>
                                                            <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                              <span style="font-family: Courier New,monospace;">@DataModel</span><span style="font-family: Courier New,monospace;">@DataModelSelection </span>
                                                            </td>
                                                            
                                                            <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                              <span style="font-family: Courier New,monospace;">javax.faces.model.ListDataModel;</span>
                                                            </td>
                                                          </tr>
                                                          
                                                          <tr>
                                                            <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                                              The annotations @DataModel and @DataModelSelection facilitates the use of JPA results into facelets pages.This is facilitated in JSF 2, to wrap the JPA result into a javax.faces.model.ListDataModel object.</p> 
                                                              
                                                              <p>
                                                                &nbsp;
                                                              </p>
                                                              
                                                              <p>
                                                                &nbsp;</td> </tr> 
                                                                
                                                                <tr>
                                                                  <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                                    The seam-booking uses a mixture of maven and ant to build.The resultant file is an EAR file.
                                                                  </td>
                                                                  
                                                                  <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                                    <p style="margin-bottom: 0cm;">
                                                                      booking uses only maven to build it, it uses the BOM org.jboss.bom:jboss-javaee-6.0-with-hibernate
                                                                    </p>
                                                                    
                                                                    <p>
                                                                      The resultant file is a WAR.</td> </tr> 
                                                                      
                                                                      <tr>
                                                                        <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                                                          WAR file are simpler to use and allows for EJB lite to be deployed in it.</p> 
                                                                          
                                                                          <p>
                                                                            &nbsp;</td> </tr> 
                                                                            
                                                                            <tr>
                                                                              <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                                                <span style="font-family: Courier New,monospace;">FacesMessages.instance().add(&#8220;Booking cancelled for confirmation number #0&#8221;, booking.getId());</span>
                                                                              </td>
                                                                              
                                                                              <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                                                <span style="font-family: Courier New,monospace;">FacesContext.getCurrentInstance().getExternalContext().getFlash().setKeepMessages(true);</span>
                                                                              </td>
                                                                            </tr>
                                                                            
                                                                            <tr>
                                                                              <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                                                                JBoss Seam allows to send messages to end user after a redirect, however for that to work, flash scope must be used, as show above.</p> 
                                                                                
                                                                                <p>
                                                                                  &nbsp;</td> </tr> 
                                                                                  
                                                                                  <tr>
                                                                                    <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                                                      <span style="font-family: Courier New,monospace;">Stateless EJB, uses JBoss Seam authenticator infrastructure defined in components.xml.</span>
                                                                                    </td>
                                                                                    
                                                                                    <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                                                      <span style="font-family: Courier New,monospace;">Uses @Picketlink annotation for authentication, also stores the user bean into<br /> http session, to be validate at the SecurityFilter. Also produces a bean named &#8220;loggedUser&#8221;,<br /> to export the authenticated</span>
                                                                                    </td>
                                                                                  </tr>
                                                                                  
                                                                                  <tr>
                                                                                    <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                                                                    </td>
                                                                                  </tr>
                                                                                  
                                                                                  <tr>
                                                                                    <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                                                      <span style="font-family: Courier New,monospace;">Send an event</span><span style="font-family: Courier New,monospace;">@In</span></p> 
                                                                                      
                                                                                      <p>
                                                                                        <span style="font-family: Courier New,monospace;">private Events events;</span>
                                                                                      </p>
                                                                                      
                                                                                      <p>
                                                                                        <span style="font-family: Courier New,monospace;">events.raiseTransactionSuccessEvent(&#8220;bookingConfirmed&#8221;);</span>
                                                                                      </p>
                                                                                      
                                                                                      <p>
                                                                                        &nbsp;
                                                                                      </p>
                                                                                      
                                                                                      <p>
                                                                                        <span style="font-family: Courier New,monospace;">Receive an event</span>
                                                                                      </p>
                                                                                      
                                                                                      <p>
                                                                                        <span style="font-family: Courier New,monospace;">@Observer(&#8220;bookingConfirmed&#8221;)</span>
                                                                                      </p>
                                                                                      
                                                                                      <p>
                                                                                        <span style="font-family: Courier New,monospace;">public void getBookings() {</span></td> 
                                                                                        
                                                                                        <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                                                          <p style="margin-bottom: 0cm;">
                                                                                            <span style="font-family: Courier New,monospace;">Send an event</span>
                                                                                          </p>
                                                                                          
                                                                                          <p style="margin-bottom: 0cm;">
                                                                                            <span style="font-family: Courier New,monospace;">@Inject</span>
                                                                                          </p>
                                                                                          
                                                                                          <p style="margin-bottom: 0cm;">
                                                                                            <span style="font-family: Courier New,monospace;">private Event<BookingEvent> bookingevent;</span>
                                                                                          </p>
                                                                                          
                                                                                          <p style="margin-bottom: 0cm;">
                                                                                            <span style="font-family: Courier New,monospace;">bookingevent.fire(new BookingEvent());</span>
                                                                                          </p>
                                                                                          
                                                                                          <p style="margin-bottom: 0cm;">
                                                                                            <span style="font-family: Courier New,monospace;">Receive an event</span>
                                                                                          </p>
                                                                                          
                                                                                          <p>
                                                                                            <span style="font-family: Courier New,monospace;">public void updateBookingList(@Observes BookingEvent bookingEvent)</span></td> </tr> 
                                                                                            
                                                                                            <tr>
                                                                                              <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                                                              </td>
                                                                                              
                                                                                              <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                                                              </td>
                                                                                            </tr></tbody> </table> 
                                                                                            
                                                                                            <p style="margin-bottom: 0cm; line-height: 100%;">
                                                                                              New classes were added
                                                                                            </p>
                                                                                            
                                                                                            <ul>
                                                                                              <li>
                                                                                                Resources.java: Produces and close the EntityManager.
                                                                                              </li>
                                                                                              <li>
                                                                                                SecurityAction.java: Control the login and logout process.
                                                                                              </li>
                                                                                              <li>
                                                                                                SecurityFilter.java: Control the access to the protected pages. This could be implemented using <a href="http://deltaspike.apache.org/security.html" target="_blank">DeltaSpike Security api</a>
                                                                                              </li>
                                                                                            </ul>
                                                                                            
                                                                                            <p>
                                                                                              Now the changes to the facelets pages and descriptors.
                                                                                            </p>
                                                                                            
                                                                                            <p>
                                                                                              There are lots of changes only to replace JBoss Seam taglibs to JSF 2 taglibs, the most commons are show below. Most of them are very intuitive to follow, so I will not explain.
                                                                                            </p>
                                                                                            
                                                                                            <table width="100%" cellspacing="0" cellpadding="4">
                                                                                              <colgroup> <col width="122*" /> <col width="134*" /> </colgroup> <tr valign="top">
                                                                                                <td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0.1cm 0cm 0.1cm 0.1cm;" bgcolor="#eeeeee" width="48%">
                                                                                                  <p align="center">
                                                                                                    <b>JBoss Seam</b>
                                                                                                  </p>
                                                                                                </td>
                                                                                                
                                                                                                <td style="border: 1px solid #000000; padding: 0.1cm;" bgcolor="#eeeeee" width="52%">
                                                                                                  <p align="center">
                                                                                                    <b>Java EE 7</b>
                                                                                                  </p>
                                                                                                </td>
                                                                                              </tr>
                                                                                              
                                                                                              <tr>
                                                                                                <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                                                                  <span style="font-family: Courier New,monospace;">Removal of JBoss Seam taglib definition</span></p> 
                                                                                                  
                                                                                                  <p>
                                                                                                    &nbsp;
                                                                                                  </p>
                                                                                                  
                                                                                                  <p>
                                                                                                    <span style="font-family: Courier New,monospace;">xmlns:s=&#8221;http://jboss.com/products/seam/taglib&#8221;</span></td> 
                                                                                                    
                                                                                                    <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                                                                    </td></tr> 
                                                                                                    
                                                                                                    <tr>
                                                                                                      <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                                                                                      </td>
                                                                                                    </tr>
                                                                                                    
                                                                                                    <tr>
                                                                                                      <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                                                                        <span style="font-family: Courier New,monospace;"><s:decorate id=&#8221;checkinDateDecorate&#8221; template=&#8221;edit.xhtml&#8221; ></span>
                                                                                                      </td>
                                                                                                      
                                                                                                      <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                                                                        <span style="font-family: Courier New,monospace;"><ui:decorate template=&#8221;edit.xhtml&#8221;></span></p> 
                                                                                                        
                                                                                                        <p>
                                                                                                          <span style="font-family: Courier New,monospace;"><ui:param name=&#8221;id&#8221; value=&#8221;checkoutDate&#8221; /></span></td> </tr> 
                                                                                                          
                                                                                                          <tr>
                                                                                                            <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                                                                                              On the template fragment edit.xhtml, needed to add the id attribute as #{id} as its value, as the template rendered leads to error of an already used id value.</p> 
                                                                                                              
                                                                                                              <p>
                                                                                                                Also, use the ui:param to send parameters to the template page.
                                                                                                              </p>
                                                                                                              
                                                                                                              <p>
                                                                                                                &nbsp;
                                                                                                              </p>
                                                                                                              
                                                                                                              <p>
                                                                                                                &nbsp;</td> </tr> 
                                                                                                                
                                                                                                                <tr>
                                                                                                                  <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                                                                                    <span style="font-family: Courier New,monospace;"><a:support id=&#8221;onblur&#8221; event=&#8221;onblur&#8221; reRender=&#8221;creditCardNameDecorate&#8221;/></span>
                                                                                                                  </td>
                                                                                                                  
                                                                                                                  <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                                                                                    <span style="font-family: Courier New,monospace;"><f:ajax render=&#8221;message_creditCardName&#8221; event=&#8221;blur&#8221; /></span>
                                                                                                                  </td>
                                                                                                                </tr>
                                                                                                                
                                                                                                                <tr>
                                                                                                                  <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                                                                                                  </td>
                                                                                                                </tr>
                                                                                                                
                                                                                                                <tr>
                                                                                                                  <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                                                                                    <span style="font-family: Courier New,monospace;"><s:button id=&#8221;cancel&#8221; value=&#8221;Cancel&#8221; action=&#8221;#{hotelBooking.cancel}&#8221;/></span>
                                                                                                                  </td>
                                                                                                                  
                                                                                                                  <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                                                                                    <span style="font-family: Courier New,monospace;"><h:commandButton id=&#8221;cancel&#8221; value=&#8221;Cancel&#8221; action=&#8221;#{hotelBooking.cancel}&#8221; immediate=&#8221;true&#8221;/></span>
                                                                                                                  </td>
                                                                                                                </tr>
                                                                                                                
                                                                                                                <tr>
                                                                                                                  <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" colspan="2" width="100%">
                                                                                                                  </td>
                                                                                                                </tr>
                                                                                                                
                                                                                                                <tr>
                                                                                                                  <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: none; padding: 0cm 0cm 0.1cm 0.1cm;" width="48%">
                                                                                                                    <span style="font-family: Courier New,monospace;"><link href=&#8221;css/screen.css&#8221; rel=&#8221;stylesheet&#8221; type=&#8221;text/css&#8221; /></span>
                                                                                                                  </td>
                                                                                                                  
                                                                                                                  <td style="border-top: none; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000; padding: 0cm 0.1cm 0.1cm 0.1cm;" width="52%">
                                                                                                                    <span style="font-family: Courier New,monospace;"><h:outputStylesheet name=&#8221;css/screen.css&#8221;/></span>
                                                                                                                  </td>
                                                                                                                </tr></tbody> </table> 
                                                                                                                
                                                                                                                <p>
                                                                                                                  &nbsp;
                                                                                                                </p>
                                                                                                                
                                                                                                                <p>
                                                                                                                  To run, you need to add a datasource named java:/bookingDatasource
                                                                                                                </p>
                                                                                                                
                                                                                                                <p>
                                                                                                                  You can <a href="/wp-content/uploads/2014/06/booking.zip">download the booking migration</a>.
                                                                                                                </p>
                                                                                                                
                                                                                                                <p>
                                                                                                                  Write a comment if there is something missing or if it helped you.
                                                                                                                </p>