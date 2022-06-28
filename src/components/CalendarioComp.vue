<template>

    <body>
        <div class="columns">
            <div class="column is-10 is-offset-1">
                <h1 class="title is-1">Calendario OneSight Marlon Erick</h1>
                <button class="button" @click="toggleWeekends">toggle weekends</button>
                <FullCalendar v-bind:options="calendarOptions" :events="EVENTS" />
            </div>
        </div>
    </body>
</template>

<script lang="ts">
import '@fullcalendar/core/vdom'
import { ref, reactive, watch } from 'vue'
import FullCalendar from '@fullcalendar/vue3'
import DayGridPlugin from '@fullcalendar/daygrid'
import TimeGridPlugin from '@fullcalendar/timegrid'
import InteractionPlugin from '@fullcalendar/interaction'
import ListPlugin from '@fullcalendar/list'

const id = ref(0)

export default {
    name: 'CalendarioComp',
    components: { FullCalendar },
    data() {
        return {
            calendarOptions: {
                plugins: [DayGridPlugin, TimeGridPlugin, InteractionPlugin, ListPlugin],
                initialView: 'dayGridMonth',
                weekends: true,
                selectable: true,
                headerToolbar: {
                    right: 'dayGridMonth,dayGridWeek,listDay'
                },
                editable: true,
                weekdens: false,
                select: (arg) => {
                    id.value = id.value + 1

                    const cal = arg.view.calendar
                    cal.unselect()
                    cal.addEvent({
                        id: `${id.value}`,
                        title: `Novo Evento ${id.value}`,
                        start: arg.start,
                        end: arg.end,
                        allDay: true
                    })
                },
                eventClick: function (info) {
                    alert('Event: ' + info.event.title);
                    alert('Coordinates: ' + info.jsEvent.pageX + ',' + info.jsEvent.pageY);
                    alert('View: ' + info.view.type);

                    // change the border color just for fun
                    info.el.style.borderColor = 'red';
                }
            }
        }
    },
    methods: {
        toggleWeekends: function () {
            // eslint-disable-next-line @typescript-eslint/ban-ts-comment     
            // @ts-ignore
            this.calendarOptions.weekends = !this.calendarOptions.weekends // toggle the boolean!
        }
    },
}

</script>

<style lang="css" >
h1 {
    padding: 1rem;
    margin: 1rem 0rem;
    text-align: center;
    border: 1px solid black;
    background-color: #CCFFE5
}
</style>